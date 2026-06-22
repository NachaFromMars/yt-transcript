---
name: yt-transcript
description: "Extract text transcripts from ANY video platform: YouTube, TikTok, Facebook, Instagram, Twitter/X, Bilibili, Twitch, Vimeo, Dailymotion, Reddit, Douyin. Use when user shares a video link and wants the text content, transcript, subtitles, or spoken words. Auto-detects platform, uses fastest method available (API → subtitles → Whisper). Triggers on: video URLs, YouTube links, TikTok links, Facebook video, lấy nội dung, transcript, lấy text từ video, subtitle, phụ đề, đọc truyện, extract text from video, get transcript, lấy truyện, transcribe."
---

# Universal Video Transcript Extractor

Extract clean text from video on **any platform** — auto-detects and uses the fastest method.

## Dependencies

```
pip install youtube-transcript-api faster-whisper
```

Also needs `yt-dlp` and `ffmpeg` on PATH.

## Supported Platforms (11+)

YouTube · TikTok · Facebook · Instagram · Twitter/X · Bilibili · Twitch · Vimeo · Dailymotion · Reddit · Douyin + anything yt-dlp supports

## Pipeline (auto-fallback)

```
URL → detect platform →
  YouTube? → youtube-transcript-api (~2s, best) →
  Any platform? → yt-dlp subtitle extraction (~10s) →
  Fallback → yt-dlp download audio + faster-whisper GPU (~5-15 min)
```

## Quick Usage

### Single video (any platform)
```bash
python scripts/universal_transcript.py "URL" --lang vi
```

### Multiple videos
```bash
python scripts/universal_transcript.py "URL1" "URL2" "URL3"
```

### Force Whisper (skip subtitle check)
```bash
python scripts/universal_transcript.py "URL" --whisper
```

### YouTube-only (lighter script, no Whisper dep)
```bash
python scripts/yt_transcript.py "URL" --lang vi
python scripts/yt_transcript.py "PLAYLIST_URL"
python scripts/yt_transcript.py "CHANNEL_URL" --channel
```

## Options

- `--lang vi` — language code (default: vi)
- `--out DIR` — output directory (default: ./transcripts/)
- `--format txt|srt|json` — output format (default: txt)
- `--whisper` — skip subtitle methods, go straight to Whisper

## Scripts

- `scripts/universal_transcript.py` — main script, all platforms, Whisper fallback
- `scripts/yt_transcript.py` — YouTube-only, lighter (no Whisper needed), supports playlists/channels

## Fallback Strategy Details

See `references/fallback-methods.md` for:
- VTT parsing details
- Whisper model options (large-v3 vs small)
- OpenAI Whisper API alternative
- Cookie handling for TikTok/Facebook

## Notes

- YouTube transcript API = fastest (no download, ~2s/video)
- yt-dlp handles 1000+ sites — if it has subtitles, we extract them
- Whisper large-v3 needs ~3GB VRAM (RTX 3090 recommended)
- Some platforms (TikTok, Facebook) may need browser cookies for download
- Script auto-tries without cookies first, then cycles chrome→firefox→edge
