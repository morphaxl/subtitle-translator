# Subtitle Translator AI

Translate subtitles to **any language** using AI. Supports OpenAI, Anthropic, Gemini, and Kimi.

## Quick Start

```bash
# Clone and install
git clone https://github.com/morphaxl/subtitle-translator-ai.git
cd subtitle-translator-ai
pnpm install

# Set your API key (pick one)
export OPENAI_API_KEY=sk-...
# or ANTHROPIC_API_KEY, GEMINI_API_KEY, KIMI_API_KEY

# Translate!
pnpm run translate movie.srt --to Spanish
```

## Features

- **Multi-provider** - OpenAI, Anthropic, Gemini, Kimi
- **Auto-detection** - Picks provider from API key automatically
- **Multi-format** - SRT, VTT, ASS/SSA
- **Video extraction** - Extract subtitles from MKV/MP4
- **Batch processing** - Translate multiple files at once
- **Whisper support** - Free local transcription (generates subtitles from audio)

---

## Translation

### Translate Subtitles

```bash
pnpm run translate <input> [options]

Options:
  -t, --to <lang>          Target language (default: Hindi)
  -f, --from <lang>        Source language (default: English)
  -p, --provider <name>    openai, anthropic, gemini, kimi
  -o, --output <path>      Output file path
  -b, --batch-size <n>     Subtitles per batch (default: 500)
```

### Examples

```bash
# Translate to Turkish
pnpm run translate movie.srt --to Turkish

# Use specific provider
pnpm run translate movie.srt --to Japanese --provider anthropic

# Different source language
pnpm run translate spanish.srt --from Spanish --to English
```

### Providers

| Provider | Default Model | Pricing |
|----------|---------------|---------|
| OpenAI | gpt-4o-mini | Per token |
| Anthropic | claude-3-5-haiku | Per token |
| Gemini | gemini-2.0-flash | Per token |
| Kimi | kimi-for-coding | Per request |

Set API key via environment:
```bash
export OPENAI_API_KEY=sk-...
export ANTHROPIC_API_KEY=sk-ant-...
export GEMINI_API_KEY=AIza...
export KIMI_API_KEY=sk-kimi-...
```

---

## Extract from Video

Extract embedded subtitles from MKV/MP4/AVI:

```bash
# List subtitle streams
pnpm run extract movie.mkv --list

# Extract stream 0
pnpm run extract movie.mkv --stream 0

# Extract all streams
pnpm run extract movie.mkv --all
```

---

## Whisper Transcription

Generate subtitles from audio/video using Whisper (runs locally, free):

```bash
# Install Whisper first
pip install -U openai-whisper

# Transcribe video to subtitles
pnpm run transcribe movie.mp4

# Use better model
pnpm run transcribe movie.mp4 --model medium
```

> **Note**: Whisper can only translate **to English**. For other languages, transcribe first then use AI translation.

---

## Complete Workflow

### MKV → Translated Subtitles

```bash
# 1. Extract subtitles
pnpm run extract movie.mkv --stream 0 -o movie.srt

# 2. Translate
pnpm run translate movie.srt --to Turkish
```

### Video Without Subtitles → Translated

```bash
# 1. Generate subtitles with Whisper
pnpm run transcribe movie.mp4

# 2. Translate
pnpm run translate movie.srt --to Hindi
```

---

## Batch Processing

```bash
# Create config
pnpm run init

# Edit jobs.yaml, then run
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

```bash
# Required
pnpm install
brew install ffmpeg  # or: apt install ffmpeg

# Optional (for Whisper transcription)
pip install -U openai-whisper
```

## API Keys

- **OpenAI**: https://platform.openai.com/api-keys
- **Anthropic**: https://console.anthropic.com/settings/keys
- **Gemini**: https://aistudio.google.com/apikey
- **Kimi**: https://kimi.com/coding/profile

## License

MIT
