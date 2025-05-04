# vt-Archiver 👋

*A self-hosted tool-chain for backing-up and browsing livestream history.*

<div align="center">
  <img src="https://pbs.twimg.com/profile_images/1873411258638331905/G6DBazwk_200x200.jpg" width="140" alt="Michi" />
</div>

*Note: To setup vt-Archiver/ properly with the correct folder structure, please download (and run) the python script located in [vt-Archiver/.github/setup/vt-Archiver_setup.py](https://github.com/vt-Archiver/.github/blob/main/setup/vt-Archiver_setup.py), this sets up the correct dir structure, and walks you through setting up each file you want with a 'nice' GUI*
---

## What is vt-Archiver?

`vt-Archiver` is a set of **small, focused Python utilities** plus a **Flask front-end** that together let you:

* **Record live streams** the moment they start  
* **Bulk-download past VODs & clips** (Twitch & YouTube)
* **Dump chat logs** (with emotes!) to SQLite
* **Archive third-party emotes** (7TV + official) for a great chat replay
* **Browse everything locally** through an HLS/MP4 player that feels like a mini-YouTube

No servers to rent, no cloud buckets to maintain – just run the scripts on your own machine or NAS and open the web UI! 
vt-Archiver is also easy to host to the wider interwebs, so if you want to do that you can do that too!

---

## Repositories inside the org

| Repo | Description | Status |
|------|-------------|--------|
| **`twitch-archiver`** | Old *v1* downloader (stable) and the ongoing *v2* rewrite (incompatible structure with the website) | ![wip](https://img.shields.io/badge/status-WIP-yellow) |
| **`youtube-archiver`** | Lean script (≈400 LOC) that pulls a single video + chat → identical folder layout | ✅ |
| **`emote-archiver`** | Fetches 7TV & official Twitch emotes, converts to WebP and writes a JSON catalogue | ✅ |
| **`archive-website`** | Flask + vanilla JS site: browse grid, custom player, lazy HLS, chat replay | ✅ |
| **`.github`** | Org-wide issue templates, workflows & **this README** | 🔧 |

All tools agree on one **folder convention**  
`persons/<streamer>/<platform>/<section>/<YYYY-MM-DDThh-mm-ssZ>_<type-char><id>_<title>/`  
so the website can discover new sessions without a database.

---

## Quick start

```bash
git clone https://github.com/vt-Archiver/twitch-archiver
cd twitch-archiver
python -m venv venv && source venv/bin/activate
pip install -r requirements.txt

# copy .env.example → .env   (fill Client-ID, tokens, etc.)
python download_streams.py   # starts recording when the channel goes live
````

Spin up the UI:

```bash
git clone https://github.com/vt-Archiver/archive-website
cd archive-website
pip install -r requirements.txt
python app.py                # → http://localhost:5000
```
*Note:* For the website to work the expected structure needs to be followed:
Archiver/websites/<streamer>/
Archiver/persons/<streamer>/
if the files are not structured like this the website UI will not work..., download the 'setup' script from the `.github` repo to setup your own local version of this easily.

---

## Useful links

* **Docs / guides:** each repo ships its own `README.md` with setup steps
* **Issue tracker:** [https://github.com/vt-Archiver/issues/issues](https://github.com/vt-Archiver/issues/issues)
* **Michi Mochievee Archive (live demo):** [the website](michimochievee-archive.win)

---

## Expected Archiver structure:
```
Archiver
├─ archiver.scripts
│  ├─ .dependencies
│  │  ├─ ffmpeg
│  │  │  ├─ ffmpeg.exe
│  │  │  ├─ ffplay.exe
│  │  │  └─ ffprobe.exe
│  │  └─ yt-dlp
│  │     └─ yt-dlp.exe
│  ├─ Archiver-emotes-v1
│  │  /See README in `Archiver-emotes-v1`
│  ├─ Archiver-twitch-v1
│  │  /See README in `Archiver-twitch-v1`
│  ├─ Archiver-twitch-v2
│  │  /See README in `Archiver-twitch-v2`
│  └─ Archiver-youtube-v1
│     /See README in `Archiver-youtube-v1`
│
├─ other.scripts
│  /See README in `Archiver-miscellaneous-scripts`
│
├─ persons
│  └─ [streamer]
│     ├─ archival_progress
│     │   /See streamtracker_gui.py in `Archiver-miscellaneous-scripts` (you should also read the readme)
│     ├─ [platform]  <- e.g twitch/youtube
│     │  └─ [type]   <- e.g vods/clips/videos/highlights etc
│     │     └─ [date]_[type-char][id]_[title]
│     │        ├─ hls
│     │        │  ├─ vod.m3u8
│     │        │  └─ vod.mp4
│     │        ├─ thumbnails
│     │        │  ├─thumbnail_00...01.jpg
│     │        │  ├─thumbnail_00...02.jpg
│     │        │  └─thumbnail_main.jpg
│     │        ├─ chat.[type].sqlite
│     │        ├─ events.[type].json
│     │        └─ metadata.[type].json
│     ├─ person
│     │  └─ icon
│     │     └─ 
│     └─ [anything else you want to store about the streamer in question that's not directly related to videos, e.g I have an 'art' folder here for the official model art]
│
└─ websites
   └─ Archiver-website-[streamer]
      /See README in `Archiver-website-michimochievee`
```
