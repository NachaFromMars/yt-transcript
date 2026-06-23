# yt-transcript — Video transcript extractor for 11+ platforms

> Extract clean text from YouTube, TikTok, Facebook, Instagram, and 7+ more. Auto-detects the fastest method: API → subtitles → Whisper fallback.

[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-blueviolet)](https://github.com/NachaFromMars)

## Overview
yt-transcript extracts text transcripts from video on 11+ platforms via an auto-fallback pipeline: YouTube transcript API (~2s) → yt-dlp subtitle extraction (~10s) → faster-whisper GPU (~5–15 min). Two scripts: `universal_transcript.py` (all platforms + Whisper) and `yt_transcript.py` (YouTube, playlist, channel).

## Features
- 11+ platforms: YouTube, TikTok, Facebook, Instagram, Twitter/X, Bilibili, Twitch, Vimeo, Dailymotion, Reddit, Douyin
- Auto-fallback: API → subtitles → Whisper GPU
- Output: txt, srt, json in `./transcripts/`
- YouTube: playlist + channel batch support

## Usage / Quick Start
```bash
pip install youtube-transcript-api faster-whisper
# also: yt-dlp + ffmpeg on PATH

python scripts/universal_transcript.py "URL" --lang vi
python scripts/yt_transcript.py "PLAYLIST_URL" --lang vi
```

## Trigger Keywords (OpenClaw)
video transcript, lấy nội dung, transcript, lấy text từ video, subtitle, phụ đề, extract text from video

## Related Skills
- [tg-voice-whisper](https://github.com/NachaFromMars/tg-voice-whisper) — voice message transcription

---
Part of the [NachaFromMars](https://github.com/NachaFromMars) OpenClaw skill ecosystem.
