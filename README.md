# tv-remote

A phone-friendly web remote for a **Sony BRAVIA** (Android TV): wallpapers and slideshows, app shortcuts, and remote keys — from Safari on the same Wi-Fi, no app install.

Moved out of [prabodh1194/agent-setup](https://github.com/prabodh1194/agent-setup) (originally added in commit `d39171f`).

## What you get

- **tvremote** — a local web server (`:8765`) serving a mobile remote UI with a token-protected link. Big buttons for power, volume, d-pad/OK, back/home, apps (Netflix, Prime, JioHotstar, YouTube, Apple TV…), wallpaper slideshow and one-tap home-screen shortcuts.
- **tvwall** — the CLI behind it: find the TV by mDNS, push an image over ADB, run a slideshow.
- **tvremote.html** — the UI shell (cached thumbnails, dark AMOLED-ish theme, add-to-home-screen meta).

## Requirements

- macOS or Linux with Python 3.9+ and [`uv`](https://docs.astral.sh/uv/) (the scripts are self-contained `uv run` scripts).
- `adb` on `PATH` (Android platform tools).
- A Sony BRAVIA with **Settings → Device Preferences → About → Build** tapped 7× to enable Developer options, then **ADB debugging** enabled.
- The TV and the Mac on the same Wi-Fi.

## Run

```sh
./tvremote                      # serve on :8765, prints the iPhone URL
./tvremote --dir ~/Pictures/tv  # image folder
./tvremote --port 9000
```

Open the printed URL on the phone (same Wi-Fi), then **Share → Add to Home Screen**. The `?t=` token is private; rotate it with `rm ~/.cache/tvremote/token` and restart.

```sh
./tvwall IMAGE.png          # show one image
./tvwall --find             # print the TV's current IP
./tvwall --every 20 *.png   # slideshow
```

Thumbnails and the token live in `~/.cache/tvremote/`; the TV IP cache in `~/.cache/tvwall_ip`.

## Notes

- The default wallpaper folder points at an iCloud `wallpaper/diwali/4k` path; pass `--dir` for your own.
- ADB pairing must be accepted on the TV the first time.
