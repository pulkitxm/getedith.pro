# `ed tools`

`ed tools` manages the command line programs Edith's extensions run: which ones
this Mac has, where they came from, and which extension wants each one. It
installs a missing tool for you, updates the ones Edith installed, and removes
them again. The Tools section in Settings drives the same installer.

`ed tools` with nothing after it runs `ed tools ls`, and `ed tools list` is the
same command. Every verb runs in the Edith app, so the app must be running or
able to start.

## At a glance

| Command | What it does |
| --- | --- |
| [`ed tools ls`](./ls.md) | Lists every tool with its state, version, source and the extensions that use it. |
| [`ed tools install <tool>`](./install.md) | Installs one tool, or reports where it already is. |
| [`ed tools update <tool>`](./update.md) | Updates a tool Edith installed, or a Homebrew copy. |
| [`ed tools remove <tool>`](./remove.md) | Removes a tool Edith installed. Previews unless `--yes` is passed. |

## The tools

| `id` | Name | Used by | How `install` gets it |
| --- | --- | --- | --- |
| `homebrew` | Homebrew | Homebrew, App Updates | the signed `Homebrew.pkg` from the latest `Homebrew/brew` release, opened in Installer |
| `herdr` | Herdr | Agents | the `herdr-macos-*` binary from the latest `herdrdev/herdr` release |
| `quinjet` | Quinjet | Code Review | `brew install pulkitxm/tap/quinjet` when Homebrew is present, otherwise the `quinjet-macos-*` binary from `pulkitxm/quinjet` |
| `gh` | GitHub CLI | LaTeX, Code Stats, Code Review | `brew install gh` when Homebrew is present, otherwise the official `gh_<version>_macOS_*.zip` from `cli/cli` |
| `git` | Git | Code Stats, Cleaner | Apple's Command Line Tools installer |
| `yt-dlp` | yt-dlp | Music, Downloads | always the `yt-dlp_macos` binary from the latest `yt-dlp/yt-dlp` release |
| `ffmpeg` | FFmpeg | Music, Studio, Downloads | `brew install ffmpeg`, installing Homebrew first when it is missing |
| `deno` | Deno | Music, Downloads | the `deno-<arch>-apple-darwin.zip` from the latest `denoland/deno` release |
| `gallery-dl` | gallery-dl | Music, Downloads | `brew install gallery-dl`, installing Homebrew first when it is missing |
| `tectonic` | Tectonic | LaTeX | the `tectonic-<version>-<arch>-apple-darwin.tar.gz` from the latest `tectonic-typesetting/tectonic` release |
| `latexmk` | TeX Live | LaTeX | not installable; detected when `latexmk` is present |
| `ripgrep` | ripgrep | Bifrost | `brew install ripgrep` when Homebrew is present, otherwise the `ripgrep-<version>-<arch>-apple-darwin.tar.gz` from `BurntSushi/ripgrep` |
| `sshfs` | sshfs | Machines | the signed FUSE-T and sshfs packages from `macos-fuse-t`, opened in Installer one after the other |

## Where tools go

Direct downloads land in Edith's own tools folder, `Tools/bin` inside Edith's
Application Support folder (`~/Library/Application Support/Edith/Tools/bin` for
the release app; development builds use their own slot). Edith gives every
extension that folder as `EDITH_TOOLS_DIRECTORY` and searches it first, so a
tool installed once is found by every extension, by readiness checks and by
`ed tools ls`.

A download is verified before it is used. Edith reads the release from the
GitHub API, requires the asset's published SHA-256 digest or the release's
checksum file (and both must agree when both exist), hashes the file while it
streams into `Tools/.staging`, unpacks zip archives in process and tar.gz
archives with the system `tar`, then renames the binary into `Tools/bin`. A
mismatch, a cancelled install or a failure removes the staged files. Installer
packages must carry a valid Apple Developer ID Installer signature from the
publisher's pinned team (Homebrew `927JGANW46`, FUSE-T and sshfs `6DY7Z4SVDZ`)
and be notarized by Apple, even when the release publishes no digest.

Homebrew installs run with `NONINTERACTIVE=1` and `HOMEBREW_NO_AUTO_UPDATE=1`.
When a tool only comes from Homebrew and Homebrew is missing, Edith installs
Homebrew first through its signed package and continues once Installer
finishes.

What Edith installed is recorded in `Tools/installed.json` (id, version, method,
paths, source and date). Only those tools can be removed or updated through
Edith. Tools you installed yourself are listed and used, never touched. The
host also writes each tool's state to `ExtensionState/Tools/status.json`, which
extensions read to show install progress.

## Search order

Edith looks for a tool in these directories, first match wins:

```
<Edith>/Tools/bin
<every directory in your login shell PATH>
~/.local/bin
~/.cargo/bin
~/.nvm/versions/node/<version>/bin
~/.nvm/current/bin
/opt/homebrew/bin
/usr/local/bin
/Library/TeX/texbin
/usr/bin
/bin
/usr/sbin
/sbin
<every directory already in Edith's own PATH>
```

Duplicates are dropped, and directories under `/Volumes` are skipped unless
they are inside your home folder. `/usr/bin/git` only counts when Xcode or the
Command Line Tools back it.

## Exit codes

| Code | When this group produces it |
| --- | --- |
| 0 | The listing printed, the tool was installed, updated or removed, or it was already there. |
| 2 | An unknown verb, an unknown flag, a missing tool id, or a tool id that is not in the table above. |
| 1 | The install, update or removal could not finish. The error says why in one sentence, for example `The download did not match its published checksum.` |

## Where to go next

- [`ed extensions`](../extensions/README.md), whose `status` and `doctor`
  output names a missing tool and the `ed tools install` command for it.
- [`ed download`](../download/README.md), the queue yt-dlp serves.
- [All `ed` commands](../README.md)
