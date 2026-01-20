# live2d-voice-chat

Live2D 캐릭터 기반 AI 음성 대화 시스템

## 시스템 구조

### 대화 파이프라인
```python
# 1. 사용자 입력 → GPT-4o
user_message → conversation_history.append()

response = openai.chat.completions.create(
    model="gpt-4o",
    messages=conversation_history,
    max_tokens=1024,
    temperature=0.7
)

# 2. 이중 언어 응답 파싱
japanese_response, korean_response = response.split('///')

# 3. 일본어 → VOICEVOX TTS
audio_query = POST /audio_query?speaker=7&text={japanese}
synthesis = POST /synthesis?speaker=7 (audio_query)

# 4. 클라이언트 전송
return {
    "message": korean_response,  # 화면 표시
    "audio": "/audio"            # 음성 재생
}
```

### 캐릭터 시스템 프롬프트
```python
# 고정 제약 (FIXED_CONSTRAINTS)
- 반드시 '///' 구분자 사용
- 일본어 /// 한국어 형식 강제
- 내용 생략 금지

# 캐릭터 설정 (CHARACTER_PROMPT)
이름: ヒカリ (히카리)
나이: 17세
외모: 긴 검은 머리, 녹색 눈동자, 교복
성격: 친절하고 지적이며 약간 내향적
취미: 독서, 프로그래밍, 천체 관측
특기: 암기력, 논리적 사고
말투: 정중하지만 친구에게는 편한 말투

# 출력 예시
はい、私も読書が大好きです。/// 네, 저도 독서를 정말 좋아해요.
```

### VOICEVOX 연동
```python
# Docker 엔진 필수
docker run -p 50021:50021 voicevox/voicevox_engine:cpu-ubuntu20.04-latest

# TTS 생성 (2단계)
1. audio_query = POST http://localhost:50021/audio_query
   params: { speaker: 7, text: japanese_text }

2. synthesis = POST http://localhost:50021/synthesis
   params: { speaker: 7 }
   body: audio_query (JSON)
   
# 출력: WAV 파일
```

### Live2D 렌더링
```javascript
// Cubism SDK 4.0
model_path = `/static/models/live2d/{MODEL_NAME}/{MODEL_NAME}.model3.json`

// 립싱크 (음성 재생 시)
- 오디오 재생 시작 → 입 모션 트리거
- 음성 종료 → 기본 표정 복귀

// 표정 변화
- 대화 시작: 미소
- 응답 대기: 기본 표정
```

## 기술 스택

- FastAPI (비동기 처리)
- OpenAI API (GPT-4o)
- VOICEVOX (일본어 TTS)
- Live2D Cubism SDK
- httpx (비동기 HTTP)
- Jinja2 (템플릿)
- Poetry (의존성 관리)

## 설치

```bash
# 1. VOICEVOX 엔진 실행
docker run -d -p 50021:50021 voicevox/voicevox_engine:cpu-ubuntu20.04-latest

# 2. 의존성 설치
poetry install

# 3. 환경 변수 설정
echo "OPENAI_API_KEY=..." > .env

# 4. 서버 실행
poetry run uvicorn app.main:app --reload
```

## 환경 변수

```env
OPENAI_API_KEY=...
VOICE_VOXS_URL=http://localhost:50021
LIVE2D_MODEL_NAME=hiyori  # 모델 폴더명
```

## 구조

```
app/
├── main.py                 # FastAPI 엔트리포인트
├── config/
│   ├── settings.py         # 환경 설정
│   └── prompts.py          # 캐릭터 프롬프트
├── utils/
│   ├── openai_helper.py    # GPT-4o 연동
│   └── audio.py            # VOICEVOX TTS
├── templates/
│   └── chat.html           # 채팅 UI
└── models/
    └── live2d/
        └── {MODEL_NAME}/   # Live2D 모델 파일
            ├── *.model3.json
            ├── textures/
            └── motions/
```

## API 엔드포인트

- `GET /` - 채팅 UI
- `GET /chat?message={text}` - 대화 생성
- `GET /audio` - 음성 파일 다운로드
- `GET /live2d_model_info` - 모델 경로 조회
