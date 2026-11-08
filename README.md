# Aigo releases

Windows builds of **Aigo**: remote control for coding agents and terminals. Aigo runs Claude Code,
Codex, OpenCode, Pi (or any CLI) in persistent sessions on your PC. You can watch them, chat with
them, approve their requests and resume them from the desktop app, a browser, or the Aigo iPhone app.
It needs no account and no server: everything runs on your own machine.

This repository only hosts the release files. The source code is private.

## Install (Windows 10/11, no administrator rights)

1. Open the [latest release](https://github.com/YaselMS/aigo-releases/releases/latest) and download
   `Aigo-<version>-win-x64.zip`.
2. Extract the zip into a folder.
3. In that folder, run:

   ```
   powershell -ExecutionPolicy Bypass -File install.ps1
   ```

4. Open **Aigo** from the Start Menu.

The installer puts Aigo in `%LOCALAPPDATA%\Programs\Aigo` and adds the `aigo` CLI to your user PATH.
It also creates a Start Menu shortcut, starts Aigo when you log on, and installs hooks for the coding
agents it finds. Options:

- `-NoHooks`: do not install agent hooks.
- `-NoAutostart`: do not start Aigo at logon.
- `-Uninstall`: remove Aigo. Your data in `%LOCALAPPDATA%\Aigo` is kept.

### SmartScreen

The executables are not code-signed yet, so Windows SmartScreen may warn about them the first time
("Windows protected your PC"). Click **More info**, then **Run anyway**. If Windows marked the
downloaded zip as blocked, right-click it, choose **Properties**, tick **Unblock**, then extract it again.

## Updates

Aigo checks this repository for new releases at start and every 6 hours. To update:

- open **Settings > Updates** and click **Install and restart**, or
- run `aigo update` in a terminal (`aigo update -check` only reports).

Before installing, the updater checks the SHA-256 of the download against the release's
`latest.json`. Running terminal sessions end when Aigo restarts. Agent conversations can be
resumed afterwards. Auto-install is off by default; you can turn it on in Settings > Updates.

## Verify a download

Each release has a `latest.json` with the SHA-256 of the zip and of every file inside it:

```
Get-FileHash .\Aigo-<version>-win-x64.zip -Algorithm SHA256
```
