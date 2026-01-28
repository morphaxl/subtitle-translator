# Subtitle Translator AI

**Free local transcription** with Whisper + AI-powered translation with OpenAI, Anthropic, Gemini, and more.

## Highlight: Free Transcription with Whisper

Generate subtitles from any video/audio **completely free** using OpenAI's Whisper locally:

```bash
# Install Whisper (one-time)
pip install -U openai-whisper
brew install ffmpeg

# Transcribe any video to subtitles - FREE!
pnpm run transcribe movie.mp4

# Translate foreign audio to English - FREE!
pnpm run transcribe japanese_movie.mp4 --translate
```

No API keys. No costs. Runs entirely on your machine.

---

## Features

- **Free Whisper transcription** - Generate subtitles from audio/video locally
- **Multi-provider translation** - OpenAI, Anthropic, Gemini, Kimi
- **Auto-detection** - Automatically picks provider from API key
- **Multi-format** - SRT, VTT, ASS/SSA input and output
- **Video extraction** - Extract existing subtitles from MKV/MP4
- **Batch processing** - Translate multiple files with YAML config

## Quick Start

```bash
# Clone and install
git clone https://github.com/morphaxl/subtitle-translator-ai.git
cd subtitle-translator-ai
pnpm install

# FREE: Transcribe video to subtitles with Whisper
pnpm run transcribe movie.mp4

# Or translate existing subtitles (requires API key)
export OPENAI_API_KEY=sk-...
pnpm run translate movie.srt --to Spanish
```

---

## Whisper Transcription (FREE)

### Generate Subtitles from Video/Audio

```bash
pnpm run transcribe <video/audio> [options]

Options:
  -m, --model <model>      tiny, base, small, medium, large (default: base)
  -l, --language <lang>    Source language (auto-detected if omitted)
  --translate              Translate to English
  -f, --format <fmt>       Output: srt, vtt, txt, json (default: srt)
  -o, --output <dir>       Output directory
  --list-models            Show available models
```

### Examples

```bash
# Basic transcription (same language)
pnpm run transcribe podcast.mp3

# Higher quality transcription
pnpm run transcribe movie.mp4 --model medium

# Foreign video → English subtitles (FREE!)
pnpm run transcribe korean_drama.mkv --translate --model medium

# List available models
pnpm run transcribe --list-models
```

### Whisper Models

| Model | Speed | Quality | VRAM | Use Case |
|-------|-------|---------|------|----------|
| tiny | ~10x | ★★☆☆☆ | ~1GB | Quick drafts |
| base | ~7x | ★★★☆☆ | ~1GB | **Recommended** |
| small | ~4x | ★★★★☆ | ~2GB | Better accuracy |
| medium | ~2x | ★★★★★ | ~5GB | High quality, translation |
| large | 1x | ★★★★★ | ~10GB | Best accuracy |

> **Note**: Whisper translates only **TO English**. For other languages, use AI providers below.

---

## AI Translation (Paid Providers)

For translating subtitles to any language, use AI providers:

### Available Providers

| Provider | Default Model | Pricing |
|----------|---------------|---------|
| OpenAI | gpt-4o-mini | Per token |
| Anthropic | claude-3-5-haiku | Per token |
| Gemini | gemini-2.0-flash | Per token |
| Kimi | kimi-for-coding | Per request |

### Setup

```bash
# Set one API key
export OPENAI_API_KEY=sk-...
# or ANTHROPIC_API_KEY, GEMINI_API_KEY, KIMI_API_KEY

# Translate
pnpm run translate movie.srt --to Spanish
```

### Translation Examples

```bash
# Auto-detect provider from environment
pnpm run translate movie.srt --to Japanese

# Use specific provider
pnpm run translate movie.srt --to Korean --provider anthropic

# Custom batch size (default: 500)
pnpm run translate movie.srt --to Hindi --batch-size 200
```

---

## Extract Subtitles from Video

Extract embedded subtitles from MKV/MP4/AVI:

```bash
# List available subtitle streams
pnpm run extract movie.mkv --list

# Extract specific stream
pnpm run extract movie.mkv --stream 0

# Extract all streams
pnpm run extract movie.mkv --all
```

---

## Complete Workflows

### Video Without Subtitles → Translated Subtitles

```bash
# 1. Generate English subtitles with Whisper (FREE)
pnpm run transcribe movie.mp4 --model medium

# 2. Translate to target language
pnpm run translate movie.srt --to Turkish
```

### Foreign Video → Your Language

```bash
# 1. Transcribe + translate to English with Whisper (FREE)
pnpm run transcribe foreign_movie.mp4 --translate --model medium

# 2. Translate English to your language
pnpm run translate foreign_movie.srt --to Hindi
```

### MKV with Embedded Subtitles → Translated

```bash
# 1. Extract existing subtitles
pnpm run extract movie.mkv --stream 0 -o movie.srt

# 2. Translate
pnpm run translate movie.srt --to Spanish
```

---

## Batch Processing

```bash
# Create config
pnpm run init

# Edit jobs.yaml
# Run all jobs
pnpm run batch
```

**jobs.yaml:**
```yaml
defaults:
  from: English

jobs:
  - input: movie.srt
    to: Spanish
  - input: movie.srt  
    to: French
  - input: movie.srt
    to: Japanese
```

---

## Installation

### Prerequisites

- **Node.js 18+**
- **ffmpeg** - for video processing
- **Whisper** - for free transcription (optional)

```bash
# Install ffmpeg
brew install ffmpeg        # macOS
sudo apt install ffmpeg    # Linux

# Install Whisper (for free transcription)
pip install -U openai-whisper
```

### Setup

```bash
git clone https://github.com/morphaxl/subtitle-translator-ai.git
cd subtitle-translator-ai
pnpm install
```

---

## API Keys

Only needed for AI translation (not for Whisper):

- **OpenAI**: https://platform.openai.com/api-keys
- **Anthropic**: https://console.anthropic.com/settings/keys  
- **Gemini**: https://aistudio.google.com/apikey
- **Kimi**: https://kimi.com/coding/profile

---

## License

MIT
