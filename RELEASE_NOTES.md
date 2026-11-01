## Steamcord 1.43.0 — Windows Big Picture support, same zip as the Steam Deck

**One release, two hosts.** `Steamcord-for-Windows.zip` now runs on the Steam Deck
(Decky Loader, Gaming Mode) **and** on Windows (Decky Loader for Windows, Steam Big
Picture). The plugin detects the host when it starts — nothing to choose, nothing to
configure.

### New: Windows

- **Discord in Steam Big Picture on Windows 10 / 11.** Voice chat, DMs and group DMs,
  servers and text chat, QR login and the CAPTCHA solver, Steam-toast notifications,
  soundboard, Rich Presence and per-user volume work in the Quick Access Menu, driven by
  a real Vesktop just like on the Deck.
- **Vesktop is installed for you** (winget, or the official installer, silently and
  per-user — no administrator prompt) and started minimised on its own profile. A
  Vesktop you already use on the desktop is never touched.
- **One Discord per Steam account** on Windows too, with the same automatic switching.
- **Go Live on Windows** shares the primary display through Electron's own screen
  capture (video only for now).
- The QAM hides what a platform cannot do, so Windows users never see PipeWire audio
  routing, the virtual camera, in-game overlays or the evdev controller shortcut.

### Unchanged on the Steam Deck

Every Linux code path is kept as it was; the Windows logic sits behind a platform check.
The whole existing test suite still passes.

### Windows limitations (first release)

No game-audio sharing or game ↔ Discord mix, no in-plugin audio device picker (Vesktop
uses the Windows default devices), no virtual camera mode, no in-game overlays, no
controller push-to-talk, no keep-awake. Details and troubleshooting:
[docs/WINDOWS.md](docs/WINDOWS.md).

> The Windows port is new and has had limited time on real handhelds. Please report
> what you find.

### Install

- **Steam Deck / Linux:** Decky → Developer → *Install from URL* →
  `https://github.com/SilvertongueRED/Steamcord-for-Windows/releases/latest/download/Steamcord-for-Windows.zip`
- **Windows:** install [Decky Loader for Windows](https://github.com/musika08/decky-loader-windows)
  (3.3+), then Decky → Developer → *Install Plugin from URL* (same link) or
  *Install Plugin from ZIP File*.

### Upgrading

- This release adds files at the plugin's top level (`sc_platform.py`,
  `vesktop_windows.py`), so install it the normal way (URL or ZIP above) — the built-in
  updater can overwrite files but not create new ones.
- The in-plugin update check now follows **this fork's** releases instead of the
  upstream Steamcord ones, so an upstream Linux-only build can no longer replace the
  Windows-capable one.

### Under the hood

- `defaults/sc_platform.py` (host, paths, feature flags) and `defaults/vesktop_windows.py`
  (find / install / launch / stop Vesktop on Windows); `Plugin.get_platform_caps` and
  `src/platform.ts` carry the feature flags to the UI.
- CI: a Windows job runs the platform tests on a real Windows runner, and the release
  fails if the built zip is missing either the Steam Deck files or the Windows layer.

Based on [Steamcord](https://github.com/Necrosiak/Steamcord) by Necrosiak (BSD-3-Clause).
