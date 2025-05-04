# vt-Archiver 👋

*A self-hosted tool-chain for backing-up and browsing livestream history.*

<div align="center">
  <img src="https://pbs.twimg.com/profile_images/1873411258638331905/G6DBazwk_200x200.jpg" width="140" alt="Michi" />
</div>

---

## What is vt-Archiver?

`vt-Archiver` is a set of **small, focused Python utilities** plus a **Flask front-end** that together let you:

* **Record live streams** the moment they start  
* **Bulk-download past VODs & clips** (Twitch & YouTube)
* **Dump chat logs** (with emotes!) to SQLite
* **Archive third-party emotes** (7TV + official) for a great chat replay
* **Browse everything locally** through an HLS/MP4 player that feels like a mini-YouTube

No servers to rent, no cloud buckets to maintain – just run the scripts on your own machine or NAS and open the web UI, and if you want to host a website with this you should easily be able to do that too!

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
