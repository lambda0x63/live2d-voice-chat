<h1 align="center">
    live2d-voice-chat
</h1>
<p align="center">
	A real-time chat interface combining Live2D characters with LLM and Japanese voice synthesis
</p>

<h2 align="left">Key Features</h2>
- Real-time Live2D animation with lip-sync and facial expressions<br>
- AI-powered conversation using LLM-based response generation<br>
- Multi-language TTS support (Japanese and Korean)<br>
- Interactive web interface with real-time animated feedback<br>
- WebSocket-based real-time communication

<h2 align="left">Technical Highlights</h2>
- Live2D SDK integration for character animation<br>
- VOICEVOX TTS engine integration<br>
- Cross-language audio processing pipeline<br>
- Real-time WebSocket communication

<h2 align="left">Tech Stack</h2>
- **Backend**: FastAPI, Python 3.8+<br>
- **Frontend**: JavaScript, HTML/CSS<br>
- **AI/ML**: OpenAI API<br>
- **Voice Synthesis**: VOICEVOX<br>
- **Animation**: Live2D SDK<br>
- **Tools**: Poetry, Docker

<h2 align="left">Requirements</h2>
- Python 3.8+<br>
- Poetry<br>
- Docker<br>
- ffmpeg<br>
- OpenAI API key

<h2 align="left">Installation & Setup</h2>

1. **Install ffmpeg:**
   - Ubuntu: `sudo apt-get install ffmpeg`
   - macOS: `brew install ffmpeg`
   - Windows: Download from https://ffmpeg.org/download.html

2. **Start VOICEVOX Engine:**
   ~~~bash
   docker run --rm -it -p 50021:50021 voicevox/voicevox_engine:cpu-ubuntu20.04-latest
   ~~~

3. **Clone and install dependencies:**
   ~~~bash
   git clone https://github.com/lambda0x63/live2d-voice-chat.git
   cd live2d-voice-chat
   poetry install
   ~~~

4. **Configure environment:**
   Create `.env` file with:
   ~~~bash
   OPENAI_API_KEY=your_api_key_here
   ~~~

5. **Run server:**
   ~~~bash
   poetry run uvicorn app.main:app --reload
   ~~~

<h2 align="left">Usage</h2>
1. Start VOICEVOX engine (Docker container)
2. Run the application
3. Open `http://localhost:8000`
4. Chat with your Live2D character and watch it respond with voice and animation!

<h2 align="left">Customization</h2>
- **Change Live2D model**: Modify `LIVE2D_MODEL_NAME` in `app/config/settings.py`<br>
- **Change character settings**: Modify `CHARACTER_PROMPT` in `app/config/prompts.py`<br>
  (Note: Maintain `FIXED_CONSTRAINTS`)<br>
- **Model directory structure**:
  ~~~
  app/models/live2d/[YOUR_MODEL_NAME]/
  ├── model.json
  ├── textures/
  └── motions/
  ~~~

<h2 align="left">Prerequisites</h2>
- VOICEVOX must be running locally on port 50021<br>
- Live2D model files should be located in the `app/models/live2d/[YOUR_MODEL_NAME]/` directory<br>
- OpenAI API key is required for LLM functionality
