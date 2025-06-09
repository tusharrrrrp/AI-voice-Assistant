# LiveKit Voice Agent with Metrics Logging

A production-ready voice assistant built with LiveKit that features real-time speech-to-text, LLM processing, text-to-speech, and comprehensive performance metrics tracking.

## Features

- **Real-time Voice Conversation**: Natural voice interactions with minimal latency
- **Multi-provider Integration**: 
  - STT: Deepgram for speech recognition
  - LLM: Groq (Llama3-8B-8192) for intelligent responses
  - TTS: Cartesia for natural voice synthesis
- **Advanced Audio Processing**:
  - Silero VAD for voice activity detection
  - Noise cancellation with BVC
  - Multilingual turn detection
- **Comprehensive Metrics Tracking**: Automatic logging of performance metrics to Excel
- **Robust Error Handling**: Detailed logging and error recovery

## Metrics Tracked

The agent automatically tracks and logs the following performance metrics:

- **End-of-Utterance Delay**: Time to detect speech completion
- **Transcription Delay**: Speech-to-text processing time
- **Time to First Token (TTFT)**: LLM response initiation time
- **TTS Time to First Byte**: Voice synthesis start time
- **Token Counts**: Input/output tokens for cost tracking
- **Audio Duration**: Generated speech length
- **Total Latency**: End-to-end response time

All metrics are automatically saved to `~/Desktop/metrics_log.xlsx` for analysis.

## Prerequisites

- Python 3.9+
- LiveKit account and API credentials
- API keys for:
  - Deepgram (STT)
  - Groq (LLM)
  - Cartesia (TTS)

## Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd livekit-voice-agent
   ```

2. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**:
   Create a `.env.local` file in the project root:
   ```env
   LIVEKIT_URL=your_livekit_url
   LIVEKIT_API_KEY=your_api_key
   LIVEKIT_API_SECRET=your_api_secret
   DEEPGRAM_API_KEY=your_deepgram_key
   GROQ_API_KEY=your_groq_key
   CARTESIA_API_KEY=your_cartesia_key
   ```

## Usage

1. **Start the voice agent**:
   ```bash
   python voice_agent.py
   ```

2. **Connect to the room**: The agent will automatically connect to LiveKit rooms and wait for participants.

3. **Begin conversation**: Once a participant joins, the agent will greet them and begin responding to voice input.

## Configuration

### Agent Behavior
Modify the `Assistant` class instructions to customize the agent's personality and response style:

```python
instructions="You are a voice assistant created by LiveKit. Use short, polite, and clear answers."
```

### Audio Settings
Adjust voice activity detection sensitivity:

```python
min_endpointing_delay=0.5,  # Minimum silence before considering speech ended
max_endpointing_delay=5.0,  # Maximum wait time for speech continuation
```

### Model Selection
Change the LLM model in the Assistant constructor:

```python
llm=groq.LLM(model="llama3-8b-8192")  # Switch to different Groq models
```

## File Structure

```
project/
├── voice_agent.py          # Main application file
├── .env.local             # Environment variables (create this)
├── requirements.txt       # Python dependencies
├── README.md             # This file
└── logs/
    ├── voice_agent_debug003.log  # Debug logs
    └── metrics_log003.xlsx       # Performance metrics
```

## Logging

The agent provides comprehensive logging:

- **Console Output**: Real-time status updates
- **Debug Log**: Detailed logs saved to `~/Desktop/voice_agent_debug.log`
- **Metrics Excel**: Performance data in `~/Desktop/metrics_log.xlsx`

### Common Issues

1. **VAD Loading Failure**: Ensure you have sufficient system resources and internet connectivity for model downloads.

2. **API Connection Errors**: Verify all API keys are correctly set in `.env.local`.

3. **Audio Issues**: Check microphone permissions and audio device configuration.

### Debug Steps

1. Check the debug log file for detailed error messages
2. Verify environment variables are loaded correctly
3. Test individual components (STT, LLM, TTS) separately

## Performance Optimization

- **Prewarming**: The agent preloads the VAD model for faster initialization
- **Metrics Storage**: Partial metrics are stored in memory until complete for efficient Excel writing
- **Error Recovery**: Robust error handling prevents crashes from individual component failures


## Acknowledgments

- [LiveKit](https://livekit.io/) for the real-time communication platform
- [Deepgram](https://deepgram.com/) for speech-to-text services
- [Groq](https://groq.com/) for fast LLM inference
- [Cartesia](https://cartesia.ai/) for text-to-speech synthesis

## Support

For support and questions:
- Check the [LiveKit documentation](https://docs.livekit.io/)
- Review debug logs for error details
- Open an issue in this repository

---

**Note**: This is a development version. For production deployment, consider additional security measures, monitoring, and scaling configurations.
