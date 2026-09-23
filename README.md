# tools-update

Binary releases and the **auto-update feed** for the launcher and its game payload.

This repository contains **build artifacts only**. The source code is private and
is not published here.

## How the updater uses this repo

The client never calls the GitHub API. It reads stable redirect URLs, which always
resolve to the newest release:

```
https://github.com/shoxie/tools-update/releases/latest/download/manifest.json
https://github.com/shoxie/tools-update/releases/latest/download/winhttp.dll
https://github.com/shoxie/tools-update/releases/latest/download/config.json
```

Because the asset filenames are stable across releases, these URLs never change —
so there is no tag parsing, no API call and no API rate limit involved.

`manifest.json` is the contract. It carries the version and, for every file, its
size and SHA-256. The updater verifies each download against it before writing
anything to disk.

## Assets in a release

| File | Purpose |
| --- | --- |
| `manifest.json` | update contract: version plus per-file size and SHA-256 |
| `winhttp.dll` | proxy DLL for the game folder (carries the bot logic) |
| `config.json` | reference configuration template — credential fields empty |
| `ToolsUpdate-Setup.exe` | launcher installer |
| `ToolsUpdate-win32-x64-<version>.zip` | portable launcher build |
| `setup-telegram.bat` | Telegram remote-control setup — double-click |
| `telegram_setup.ps1` | the script it runs |

## Install order

1. `ToolsUpdate-Setup.exe` — installs the launcher
2. Launch it once with the game **closed** — it places `winhttp.dll` and
   `config.json`, then starts the game for you

After the first install, the launcher keeps everything current on its own.

## Note

This is a distribution endpoint for one product, not a general-purpose CDN.
