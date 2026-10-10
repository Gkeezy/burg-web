# Hide & Seek Keep — web client

**Play:** https://gkeezy.github.io/burg-web/

Greybox first-person hide-and-seek (Burg-style). Built with Godot 4.4 (HTML5, **no threads**, so it runs on GitHub Pages without SharedArrayBuffer headers).

## Play with friends (v8)

1. Open **https://gkeezy.github.io/burg-web/**, type a name, click **CREATE LOBBY**. Your browser is the host.
2. Click **COPY LINK** and send it. Links look like `https://gkeezy.github.io/burg-web/?lobby=K7QM3X`.
3. Friends open the link, type a name, press **JOIN**.
4. With 2+ players, click **START ROUND**. Keep the host tab open and visible.

No server, tunnel, port forwarding or account. Players connect peer-to-peer with WebRTC. Connection setup goes through free public relays (PeerJS cloud + ntfy.sh, encrypted with the lobby code), with public STUN only (no TURN): very strict school/office/mobile networks may fail to connect and show a "could not connect" message; retry or switch networks.

**Practice** works offline any time.

## Controls (v7)

| Who | Key | Action |
|---|---|---|
| everyone | WASD + mouse | move / look |
| everyone | Space | jump |
| everyone | Shift (hold) | sneak: slow, quiet, small hitbox |
| everyone | Q or mouse 4 | dash where you look |
| everyone | Right mouse (hold) | slingshot: swing, release to fling |
| seekers | Left mouse | tag (catch) |
| seekers | E | stun rock |
| seekers | (always on) | compass: points roughly at the nearest hider, pings every ~1 s, HOT / WARM / COLD |
| menus | Esc / Tab / F10 | free mouse / lobby / leave |

Click the game once to capture the mouse.

Version: see `version.txt` (host and friends must match; currently 0.5.0).

## Repo

Source & tooling live with the game project; this repository is the **static web export** for Pages.
