# 4knTrippyTools

**Free, open-source browser tools for music creators and video producers.**

No accounts. No uploads to any server. Everything runs locally in your browser using the Web Audio API. The Caption Generator optionally uses the Anthropic API — you bring your own key.

🔗 **Live site → [trippylonge.github.io/4knTrippyTools](https://trippylonge.github.io/4knTrippyTools)**

---

## Tools

### 01 — Track Analyzer
Drop an MP3, WAV, FLAC, or M4A file and get:
- Energy map across the full track in 15-second windows
- Colour-coded sections: intro / build / mid / peak
- BPM detection
- Copy-ready YouTube timestamp list
- 12 genre and mood tags

No API key needed. Runs entirely on Web Audio API.

---

### 02 — Video Analyzer
Upload a video and get:
- Thumbnail preview extracted from the video
- Waveform energy overview
- Timestamp map with scene labels
- Platform-specific captions for YouTube, Instagram, TikTok, and Threads
- Resolution-aware tags (vertical, widescreen, square)

No API key needed.

---

### 03 — Caption Generator *(requires Anthropic API key)*
Upload a video or audio file and Claude generates:
- YouTube title + full description + search tags
- Instagram caption
- TikTok caption
- Threads post
- 12 hashtags

Claude reads actual video frames and audio energy data to write captions that reflect your content — not just the file name. Four tone modes: Artistic, Hype, Minimal, Storytelling.

---

## Getting Started

### No-key tools (Track Analyzer + Video Analyzer)
1. Go to [trippylonge.github.io/4knTrippyTools](https://trippylonge.github.io/4knTrippyTools)
2. Click the tool you want
3. Drop your file in — results generate instantly

### Caption Generator setup
1. Create a free Anthropic account at [console.anthropic.com](https://console.anthropic.com)
2. Go to [console.anthropic.com/keys](https://console.anthropic.com/keys) and create an API key
3. On the [homepage](https://trippylonge.github.io/4knTrippyTools), paste your key into the setup card and hit **Save key**
4. The key is stored in your browser's `localStorage` — it persists across sessions and works across all three tools automatically

> Your key never touches any server. It goes directly from your browser to `api.anthropic.com` and nowhere else.

---

## Running Locally

No build step, no dependencies. Just open the HTML files directly.

```bash
git clone https://github.com/Trippylonge/4knTrippyTools.git
cd 4knTrippyTools
open index.html
```

Or serve locally to avoid any browser file:// restrictions:

```bash
npx serve .
# then open http://localhost:3000
```

---

## File Structure

```
/
├── index.html              # Landing page + API key setup
├── track-analyzer.html     # Audio timestamp + tag generator
├── video-analyzer.html     # Video timestamp + caption generator
├── caption-generator.html  # AI-powered caption generator (needs API key)
└── README.md
```

---

## How It Works

**Audio analysis pipeline:**
1. File loaded into Web Audio API via `AudioContext.decodeAudioData`
2. Raw PCM waveform sliced into 15-second windows
3. RMS (root mean square) amplitude computed per window
4. Values normalised → thresholded into 4 energy levels
5. Consecutive same-level windows collapsed into named sections
6. BPM estimated via amplitude envelope peak detection
7. Tags inferred from energy shape, BPM, duration, and aspect ratio

**Caption generation pipeline (tool 03):**
1. Video frames extracted at multiple timestamps via `<canvas>`
2. Audio energy profile computed as above
3. Frames (as base64 JPEG) + audio metadata sent to Claude via Anthropic API
4. Claude returns structured JSON with platform-specific captions and tags
5. Results rendered with one-click copy per platform

---

## Privacy

- **Track Analyzer** and **Video Analyzer**: zero network requests. All processing is local.
- **Caption Generator**: sends video frame images and audio metadata to `api.anthropic.com` using your personal API key. No data passes through any intermediary server.
- API keys are stored in `localStorage` on your own device only.

---

## Contributing

Pull requests welcome. Some ideas if you want to contribute:

- Spotify / Apple Music metadata lookup via file tags
- Batch processing multiple files at once
- Export results as PDF or CSV
- Dark/light theme toggle
- Additional platform support (LinkedIn, Pinterest, YouTube Shorts)

---

## License

MIT — free to use, fork, modify, and distribute.

---

*Built by [4knTrippy](https://github.com/Trippylonge) · Instrumental storytelling*
