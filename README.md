<h1 align="center">
    live2d-voice-chat
</h1>
<p align="center">
	A toy project implementing a simple chat interface that combines Live2D characters capable of real-time conversation based on LLM with Japanese voice synthesis
</p>

<h2 align="left">Key Features</h2>

- Real-time lip-sync display of Live2D characters
- TTS (Text-to-Speech) functionality support
- Simultaneous output in Japanese and Korean
- LLM-based response generation

<h2 align="left">Stack</h2>

- FastAPI
- Static Web
- VOICEVOX
- LLM

<h2 align="left">Requirements</h2>

- Python 3.8+
- Poetry
- Docker
- ffmpeg

<h2 align="left">Install & Run</h2>

1. ffmpeg:
   - Ubuntu: `sudo apt-get install ffmpeg`
   - macOS: `brew install ffmpeg`
   - Windows: https://ffmpeg.org/download.html
2. VOICEVOX Docker:
   ```
   docker run --rm -it -p 50021:50021 voicevox/voicevox_engine:cpu-ubuntu20.04-latest
   ```
3. dependency install:
   ```
   poetry install
   ```
4. env:
   ```
   OPENAI_API_KEY=your_api_key_here
   ```
5. run server:
   ```
   poetry run uvicorn app.main:app --reload
   ```

<h2 align="left">Customize</h2>

- Change Live2D model: Modify `LIVE2D_MODEL_NAME` in `app/config/settings.py`
- Change character settings: Modify `CHARACTER_PROMPT` in `app/config/prompts.py`
    (Note: Maintain `FIXED_CONSTRAINTS`)

<h2 align="left">Notice</h2>

- VOICEVOX must be running locally (port 50021)
- Live2D model files should be located in the `app/models/live2d/[YOUR_MODEL_NAME]/` directory
