# tools-update

Binary releases and the update feed for the ToolsUpdate launcher.

This repository contains build artifacts only.

## How the updater uses this repo

The client reads stable redirect URLs that always resolve to the newest release:

```
https://github.com/shoxie/tools-update/releases/latest/download/manifest.json
```

`manifest.json` carries the version and, for every file, its size and SHA-256.
Each download is verified against it before anything is written to disk.

## Assets in a release

| File | Purpose |
| --- | --- |
| `manifest.json` | version plus per-file size and SHA-256 |
| `winhttp.dll` | runtime module |
| `lwinject.exe` | runtime loader |
| `config.json` | default configuration template, credential fields empty |
| `ToolsUpdate-Setup.exe` | launcher installer |
| `ToolsUpdate-win32-x64-<version>.zip` | portable launcher build |
| `setup-telegram.bat`, `telegram_setup.ps1` | optional remote channel setup |

## Install

1. Run `ToolsUpdate-Setup.exe`.
2. Start the launcher; it keeps the other files up to date.
