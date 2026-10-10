# Hide & Seek Keep — web client

**Play:** https://gkeezy.github.io/burg-web/

Greybox first-person hide-and-seek (Burg-style). Built with Godot 4.4 (HTML5, **no threads** — runs on GitHub Pages without SharedArrayBuffer headers).

## Friends (quick)

1. Open **https://gkeezy.github.io/burg-web/**
2. Enter a name.
3. **Practice** works offline anytime.
4. For **live multiplayer**, the host must run a desktop WebSocket session + public tunnel, then either:
   - Paste their `wss://…/ws` into **JOIN WEB**, or
   - Share a deep link:  
     `https://gkeezy.github.io/burg-web/?ws=wss%3A%2F%2FYOUR-TUNNEL.trycloudflare.com%2Fws`

GitHub Pages only serves the game files. It cannot keep a multiplayer host process online.

## Host (desktop)

On a machine with Godot 4.4 + Node + cloudflared (see source repo `docs/PUBLIC_PLAY.md`):

```bash
# from the Burg workspace
./dev/start_public_session.sh
```

That prints a temporary `https://….trycloudflare.com` relay. Friends can use that full site **or** keep using this github.io client with:

`?ws=wss://….trycloudflare.com/ws`

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

Version: see `version.txt` (host and friends must match; currently 0.4.0).

## Repo

Source & tooling live with the game project; this repository is the **static web export** for Pages.
