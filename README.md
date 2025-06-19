<h1 align="center">
    live2d-voice-chat
</h1>
<p align="center">
    A real-time chat interface combining Live2D characters with LLM and Japanese voice synthesis
</p>

<h2 align="left">Key Features</h2>
<ul>
<li>Real-time Live2D animation with lip-sync and facial expressions</li>
<li>AI-powered conversation using LLM-based response generation</li>
<li>Multi-language TTS support (Japanese and Korean)</li>
<li>Interactive web interface with real-time animated feedback</li>
<li>WebSocket-based real-time communication</li>
</ul>

<h2 align="left">Technical Highlights</h2>
<ul>
<li>Live2D SDK integration for character animation</li>
<li>VOICEVOX TTS engine integration</li>
<li>Cross-language audio processing pipeline</li>
<li>Real-time WebSocket communication</li>
</ul>

<h2 align="left">Tech Stack</h2>
<ul>
<li><strong>Backend</strong>: FastAPI, Python 3.8+</li>
<li><strong>Frontend</strong>: JavaScript, HTML/CSS</li>
<li><strong>AI/ML</strong>: OpenAI API</li>
<li><strong>Voice Synthesis</strong>: VOICEVOX</li>
<li><strong>Animation</strong>: Live2D SDK</li>
<li><strong>Tools</strong>: Poetry, Docker</li>
</ul>

<h2 align="left">Requirements</h2>
<ul>
<li>Python 3.8+</li>
<li>Poetry</li>
<li>Docker</li>
<li>ffmpeg</li>
<li>OpenAI API key</li>
</ul>

<h2 align="left">Installation & Setup</h2>

<ol>
<li><strong>Install ffmpeg:</strong>
<ul>
<li>Ubuntu: <code>sudo apt-get install ffmpeg</code></li>
<li>macOS: <code>brew install ffmpeg</code></li>
<li>Windows: Download from https://ffmpeg.org/download.html</li>
</ul>
</li>

<li><strong>Start VOICEVOX Engine:</strong>
<pre><code>docker run --rm -it -p 50021:50021 voicevox/voicevox_engine:cpu-ubuntu20.04-latest</code></pre>
</li>

<li><strong>Clone and install dependencies:</strong>
<pre><code>git clone https://github.com/lambda0x63/live2d-voice-chat.git
cd live2d-voice-chat
poetry install</code></pre>
</li>

<li><strong>Configure environment:</strong><br>
Create <code>.env</code> file with:
<pre><code>OPENAI_API_KEY=your_api_key_here</code></pre>
</li>

<li><strong>Run server:</strong>
<pre><code>poetry run uvicorn app.main:app --reload</code></pre>
</li>
</ol>

<h2 align="left">Usage</h2>
<ol>
<li>Start VOICEVOX engine (Docker container)</li>
<li>Run the application</li>
<li>Open <code>http://localhost:8000</code></li>
<li>Chat with your Live2D character and watch it respond with voice and animation!</li>
</ol>

<h2 align="left">Customization</h2>
<ul>
<li><strong>Change Live2D model</strong>: Modify <code>LIVE2D_MODEL_NAME</code> in <code>app/config/settings.py</code></li>
<li><strong>Change character settings</strong>: Modify <code>CHARACTER_PROMPT</code> in <code>app/config/prompts.py</code><br>
(Note: Maintain <code>FIXED_CONSTRAINTS</code>)</li>
<li><strong>Model directory structure</strong>:
<pre><code>app/models/live2d/[YOUR_MODEL_NAME]/
├── model.json
├── textures/
└── motions/</code></pre>
</li>
</ul>

<h2 align="left">Prerequisites</h2>
<ul>
<li>VOICEVOX must be running locally on port 50021</li>
<li>Live2D model files should be located in the <code>app/models/live2d/[YOUR_MODEL_NAME]/</code> directory</li>
<li>OpenAI API key is required for LLM functionality</li>
</ul>
