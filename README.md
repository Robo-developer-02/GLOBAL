# GLOBAL
THIS IS THE CODE WHICH WAS RUNNING IN MABFM SCHOOL'S PARENTS MEETING.


# RoboBot — AI Speech-to-Speech Chatbot

An AI-powered voice assistant that listens, thinks, and speaks back — in **English or Hindi**, switching languages automatically every message.

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| STT (Speech-to-Text) | Groq Whisper (`whisper-large-v3`) |
| LLM (AI Brain) | Groq LLaMA 3.3 70B (`llama-3.3-70b-versatile`) |
| TTS (Text-to-Speech) | Microsoft Edge TTS (`edge-tts`) — 100% free |

---

## Features

- 🎙️ **Voice Activity Detection (VAD)** — automatically detects when you start and stop speaking
- 🌐 **Bilingual** — speak in English or Hindi; RoboBot detects and replies in the same language
- 😴 **Wake Word** — says "Hello" or "Hey" to activate from idle mode
- ⏱️ **Auto-idle** — goes to sleep after 10 seconds of silence; say the wake word to resume
- 🔊 **Natural TTS voices** — Jenny (EN) and Swara (HI) by default, easily swappable

---

## Follow these steps to run

### Step 1: Create a virtual environment
```bash
python -m venv robobot-env
```

### Step 2: Activate it
```bash
robobot-env\Scripts\activate     # Windows (PowerShell)
source robobot-env/bin/activate  # Linux / macOS
```

### Step 2.1: Bypass execution policy (Windows only)
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

### Step 3: Upgrade pip
```bash
pip install --upgrade pip
```

### Step 4.1: Install all core dependencies
```bash
python -m pip install groq edge-tts pygame sounddevice soundfile numpy
```

### Step 4.2: Install python-dotenv
```bash
python -m pip install python-dotenv
```

### Step 5: Set your Groq API key

Create a `.env` file in the project root and add:
```
GROQ_API_KEY=your_key_here
```
Get your free API key at → https://console.groq.com

### Step 6: Run the chatbot
```bash
python robobot.py
```

---

## All Dependencies at a Glance

| Package | Purpose |
|---------|---------|
| `groq` | Groq API client — STT (Whisper) + LLM (LLaMA) |
| `edge-tts` | Microsoft Edge TTS — free text-to-speech |
| `pygame` | Plays the TTS audio output |
| `sounddevice` | Captures microphone input |
| `soundfile` | Reads/writes `.wav` audio files |
| `numpy` | Audio array processing & RMS energy calculation |
| `python-dotenv` | Loads `GROQ_API_KEY` from `.env` file |

---

## Configuration (inside `robobot.py`)

| Variable | Default | Description |
|----------|---------|-------------|
| `ENERGY_THRESHOLD` | `0.10` | Mic sensitivity — raise if background noise triggers false starts |
| `SILENCE_AFTER_SPEECH` | `1.2s` | Pause duration that ends your turn |
| `IDLE_TIMEOUT` | `10.0s` | Silence before going idle |
| `TTS_VOICE_EN` | `en-US-JennyNeural` | English voice (swap to `en-US-GuyNeural` for male) |
| `TTS_VOICE_HI` | `hi-IN-SwaraNeural` | Hindi voice (swap to `hi-IN-MadhurNeural` for male) |
| `WAKE_WORDS` | `["hello", "hey"]` | Words that wake the bot from idle |

---

## State Machine

```
IDLE ──(wake word)──► LISTENING ──(speech detected)──► SPEAKING
  ▲                       │                                │
  └──────(10s silence)────┘◄───────────────────────────────┘
```

---

## Notes

- A working **microphone** is required.
- Requires an active **internet connection** (Groq API + Edge TTS are cloud-based).
- The Groq free tier is generous — no credit card needed to get started.
