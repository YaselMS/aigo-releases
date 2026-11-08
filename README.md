# Aigo releases

Windows builds of **Aigo**: remote control for coding agents and terminals. Aigo runs Claude Code,
Codex, OpenCode, Pi (or any CLI) in persistent sessions on your PC. You can watch them, chat with
them, approve their requests and resume them from the desktop app, a browser, or the Aigo iPhone app.
It needs no account and no server: everything runs on your own machine.

This repository only hosts the release files. The source code is private.

## Install (Windows 10/11)

**No administrator rights needed.** Aigo installs for the current Windows user only.

Open PowerShell (Start menu, type `PowerShell`, press Enter) and paste this line:

```powershell
irm https://github.com/YaselMS/aigo-releases/releases/latest/download/get.ps1 | iex
```

It downloads the latest release, checks its SHA-256 against the release's `latest.json`, installs
Aigo and starts it. Next time, open **Aigo** from the Start Menu.

**Don't use PowerShell?** Download
[Install-Aigo.cmd](https://github.com/YaselMS/aigo-releases/releases/latest/download/Install-Aigo.cmd)
and double-click it. It runs the same installer. Windows may warn first because the file was
downloaded: click **More info**, then **Run anyway**.

Options for the one-liner (set them before running it, in the same window):

```powershell
$env:AIGO_NOHOOKS = 1       # do not install agent hooks
$env:AIGO_NOAUTOSTART = 1   # do not start Aigo at logon
$env:AIGO_NOSTART = 1       # do not start Aigo right after installing
```

The installer puts Aigo in `%LOCALAPPDATA%\Programs\Aigo` and adds the `aigo` CLI to your user PATH.
It also creates a Start Menu shortcut, starts Aigo when you log on, and installs hooks for the coding
agents it finds.

### Alternative: install from the zip

1. Open the [latest release](https://github.com/YaselMS/aigo-releases/releases/latest) and download
   `Aigo-<version>-win-x64.zip`.
2. If Windows marked the zip as blocked, right-click it, choose **Properties**, tick **Unblock**.
3. Extract the zip into a folder.
4. In that folder, run:

   ```
   powershell -ExecutionPolicy Bypass -File install.ps1
   ```

   Options: `-NoHooks`, `-NoAutostart`, `-NoStart`.
5. Open **Aigo** from the Start Menu.

### Firewall: allow the phone to connect

The first time your phone connects, Windows may ask whether to allow Aigo on the network. Click
**Allow** for **Private networks**. On a standard (non-administrator) Windows account this prompt
needs an administrator once. If you only use Aigo on the PC itself, you can skip it.

### SmartScreen

The executables are not code-signed yet, so Windows SmartScreen may warn about them the first time
("Windows protected your PC"). Click **More info**, then **Run anyway**. The one-line installer
unblocks the files for you, so this should not appear when you install that way.

## Updates

Aigo checks this repository for new releases at start and every 6 hours. To update:

- open **Settings → Updates** and click **Install and restart**, or
- run `aigo update` in a terminal (`aigo update -check` only reports), or
- run the install one-liner again.

Auto-install is **off by default**; you can turn it on in **Settings → Updates**. Before installing,
the updater checks the SHA-256 of the download against the release's `latest.json`. Running terminal
sessions end when Aigo restarts. Agent conversations can be resumed afterwards.

## Uninstall

In PowerShell:

```powershell
$env:AIGO_UNINSTALL = 1; irm https://github.com/YaselMS/aigo-releases/releases/latest/download/get.ps1 | iex
```

Or, from an extracted release zip: `powershell -ExecutionPolicy Bypass -File install.ps1 -Uninstall`.

This removes the program, the Start Menu shortcut, the logon start, the agent hooks and the PATH
entry. Your data in `%LOCALAPPDATA%\Aigo` is kept; delete that folder too to remove everything.

## Verify a download

Each release has a `latest.json` and a `SHA256SUMS.txt` with the SHA-256 of the zip and of every file
inside it:

```
Get-FileHash .\Aigo-<version>-win-x64.zip -Algorithm SHA256
```
