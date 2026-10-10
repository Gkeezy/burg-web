# Public play (v8: browser-hosted lobbies)

**https://gkeezy.github.io/burg-web/** (repo: https://github.com/Gkeezy/burg-web)

No server, tunnel, port forwarding or account is needed. Whoever creates the lobby
hosts the match in their own browser tab.

## Play with friends
1. Open https://gkeezy.github.io/burg-web/, type a name and click **CREATE LOBBY**.
2. In the lobby panel click **COPY LINK**. It copies
   `https://gkeezy.github.io/burg-web/?lobby=CODE` (it shows "Copied!"; if the browser
   blocks the clipboard, the link is selected in the text box: press Ctrl+C / ⌘C).
   The 6-letter code is also shown, and friends can type it under **JOIN A FRIEND'S LOBBY**.
3. Friends open the link, type a name and press **JOIN** (or Enter).
4. With 2+ players the host sets the options and clicks **START ROUND**.

The host must keep the tab open, and preferably visible: browsers pause background tabs,
which freezes the match for everyone. If the host closes the tab, everyone goes back to
the menu with "Host left the game". Friends can join mid-round (as spectators until the
next round), and anyone can invite more people with the same link.

URL extras: `&name=Ana` pre-fills the name, `&autojoin=1` joins without the prompt.

## How it works
- **Game traffic:** WebRTC data channels, peer-to-peer between each friend and the host
  (Godot `WebRTCMultiplayerPeer` in server/client mode). The host's browser runs the
  authoritative match logic (rounds, tags, stun, catches) and relays state, exactly
  like the old desktop listen server.
- **Signaling (only while connecting):** two free, account-less public relays at once,
  both on port 443: the **PeerJS cloud broker** (`0.peerjs.com`) and **ntfy.sh**. Every
  message is sent on both and de-duplicated. Relay ids/topics are a hash of the lobby
  code, and every payload is AES-256 encrypted with a key derived from the code, so
  the relays (or anyone watching them) can't read or inject offers without the code.
- **NAT traversal:** public STUN servers (`stun.l.google.com:19302`,
  `stun.cloudflare.com:3478`). There is **no TURN relay** (no free account-less TURN
  exists), so peers behind very strict NATs/firewalls (some school, office, hotel or
  mobile-data networks) may fail to connect. They then get "Could not connect to the
  host peer-to-peer…" after ~25 s; retry, or switch networks (e.g. home Wi-Fi or a
  phone hotspot). A wrong or closed lobby gives "Lobby CODE not found" after ~20 s.

## Version check
The live page's `<meta name="burg-version">` and `version.txt` should say `0.5.0`.
Host and friends must run the same version (others are told to reload).

## Why no threads on web
Export uses `variant/thread_support=false`, so the game runs on GitHub Pages without
COOP/COEP headers (Pages can't set those).

## Desktop / LAN (advanced)
The desktop build can't host browser lobbies (WebRTC isn't bundled for desktop). Under
**ADVANCED** in the menu it still has LAN play (ENet, UDP 7777) and the old WebSocket
host (`--host-ws`), which is no longer needed for browser play.

## Controls (v7, same in browser and desktop)

| Who | Key | Action |
|---|---|---|
| everyone | WASD + mouse | move / look |
| everyone | Space | jump |
| everyone | Shift (hold) | sneak: slow, quiet, small hitbox |
| everyone | Q or mouse 4 | dash where you look |
| everyone | Right mouse (hold) | slingshot: swing, release to fling |
| seekers | Left mouse | tag (catch) |
| seekers | E | stun rock |
| seekers | — | compass at the bottom of the screen points roughly at the nearest hider (pings ~1 s; HOT / WARM / COLD) |
| menus | Esc / Tab / F10 | free mouse / lobby panel / leave |

Browser tip: click the game once to capture the mouse (browsers only allow that after a
click). Some browsers treat mouse 4 as "Back"; Q always works.
