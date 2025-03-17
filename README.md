# Distil-Whisper for FastRTC

A PyPI package that wraps Hugging Face's Distil-Whisper model for speech-to-text (STT) transcription, compatible with the FastRTC STTModel protocol.

## Installation

```bash
pip install distil-whisper-fastrtc
```

For audio file loading capabilities, install with the audio extras:

```bash
pip install "distil-whisper-fastrtc[audio]"
```

For development:

```bash
pip install "distil-whisper-fastrtc[dev]"
```

## Usage

### Basic Usage

```python
from distil_whisper_fastrtc import get_stt_model
import numpy as np

# Create the model (downloads from HF if not cached)
model = get_stt_model()

# Example: Create a sample audio array (actual audio would come from a file or mic)
sample_rate = 16000
audio_data = np.zeros(16000, dtype=np.float32)  # 1 second of silence

# Transcribe
text = model.stt((sample_rate, audio_data))
print(f"Transcription: {text}")
```

### Loading Audio Files

If you've installed with the audio extras:

```python
from distil_whisper_fastrtc import get_stt_model, load_audio

# Load model
model = get_stt_model()

# Load audio file (automatically resamples to 16kHz)
audio = load_audio("path/to/audio.wav")

# Transcribe
text = model.stt(audio)
print(f"Transcription: {text}")
```

### Using with FastRTC

```python
from distil_whisper_fastrtc import get_stt_model

# Create the model
whisper_model = get_stt_model()

# Use within FastRTC applications
# (Follow FastRTC documentation for integration details)
```

## Available Models

You can choose from different model sizes:

- `distil-whisper/distil-small.en` (default, English only, fastest)
- `distil-whisper/distil-medium.en` (English only, better quality)
- `distil-whisper/distil-large-v2` (English highest quality)
- `distil-whisper/distil-large-v3` (Latest version, best quality)

Example:
```python
from distil_whisper_fastrtc import get_stt_model

# Choose a larger model
model = get_stt_model("distil-whisper/distil-large-v2")
```

## Advanced Configuration

You can configure the model with various parameters:

```python
from distil_whisper_fastrtc import DistilWhisperSTT

# Configure with specific device and precision
model = DistilWhisperSTT(
    model="distil-whisper/distil-medium.en",
    device="cuda",  # Use GPU if available
    dtype="float16"  # Use half precision for faster inference
)
```

## Requirements

- Python 3.8+
- PyTorch 1.10+
- transformers 4.30+
- numpy 1.20+
- accelerate 0.20+ (for faster inference)
- librosa 0.9+ (optional, for audio file loading)

## Development

Clone the repository and install in development mode:

```bash
git clone https://github.com/yourusername/distil-whisper-fastrtc.git
cd distil-whisper-fastrtc
pip install -e ".[dev,audio]"
```

Run tests:

```bash
pytest tests/
```

## License

MIT
