## Steamcord 1.43.2 - Windows fixes, now tested on a real PC

**Steamcord now runs on Windows.** Since 1.43.1 the Windows build gets past
"Initializing", and it has been tested on a Windows 11 PC in Steam Big Picture: QR login
and voice chat work. The same zip still runs on the Steam Deck, which is unchanged.

### Fixed

- **Windows: no more giant Steamcord log.** When the Discord client failed to start, each
  retry wrote the whole injected script (about 250 KB) into the log every 2 seconds. On
  1.43.0 that grew the log to hundreds of MB in a few hours. The retry message is now short.
- **UTF-8 everywhere.** The Steam Deck-only helpers (overlay, Go Live relay, controller
  watcher, screen-cast shim) now also read and write their files as UTF-8, like the rest of
  the backend since 1.43.1.

### Tests

- The UTF-8 check now covers every backend file, with no skip list.
- New checks that the injected scripts are valid UTF-8 and that the start-up retry log line
  stays short.

### Install / upgrade

- **Windows:** in Big Picture, Decky -> Developer -> *Install Plugin from URL*:
  `https://github.com/SilvertongueRED/Steamcord-for-Windows/releases/latest/download/Steamcord-for-Windows.zip`
  (or *Install Plugin from ZIP File*). If the panel still says "Initializing" after
  updating, restart Steam so the plugin starts fresh.
- **Coming from 1.43.0 on Windows:** you can delete the old, very large log in
  `%USERPROFILE%\homebrew\logs\Steamcord`.
- **Steam Deck / Linux:** Decky -> Developer -> *Install from URL* (same link). No
  behaviour change.

Windows requirements, what works on each host and troubleshooting:
[docs/WINDOWS.md](https://github.com/SilvertongueRED/Steamcord-for-Windows/blob/main/docs/WINDOWS.md).

**Full changelog:** [v1.43.1...v1.43.2](https://github.com/SilvertongueRED/Steamcord-for-Windows/compare/v1.43.1...v1.43.2)

Based on [Steamcord](https://github.com/Necrosiak/Steamcord) by Necrosiak (BSD-3-Clause).
