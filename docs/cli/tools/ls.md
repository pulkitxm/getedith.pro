# `ed tools ls`

Lists every tool Edith's extensions use.

Usage:

```
ed tools ls [--refresh] [--json]
```

Options:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--refresh` | flag | off | Checks GitHub for newer releases of tools Edith installed, instead of using the answer cached for up to 24 hours. |
| `--json` | flag | off | Emits one JSON array on stdout. |

Each tool that is found is asked for its version with a five second limit.
Tools Edith installed are also checked for updates: direct downloads against
the latest release tag, Homebrew installs with `brew outdated`.

`--json` shape, one object per tool in catalog order:

```json
{
  "id": "yt-dlp",
  "name": "yt-dlp",
  "purpose": "Downloads video and audio from websites.",
  "usedBy": ["music", "downloads"],
  "state": "installed",
  "version": "2026.10.26",
  "latestVersion": null,
  "path": "/Users/me/Library/Application Support/Edith/Tools/bin/yt-dlp",
  "origin": "edith",
  "installedByEdith": true,
  "method": "direct",
  "installable": true
}
```

`state` is one of:

| Value | Meaning |
| --- | --- |
| `installed` | Found and answered its version check. |
| `outdated` | Installed by Edith and a newer version exists; `latestVersion` names it. |
| `missing` | Not found anywhere Edith looks. |
| `broken` | Found, but its version check failed or timed out. |
| `installing` | Edith is installing it right now. |
| `detectOnly` | Not found, and Edith cannot install it (TeX Live). |

`origin` says where the found copy lives: `edith` (Edith's tools folder),
`homebrew`, `system`, or `other`. `method` is `direct`, `homebrew` or `package`
for tools Edith installed and `null` otherwise.

Examples:

```
ed tools ls
ed tools ls --refresh
ed tools ls --json | jq -r '.[] | select(.state == "missing") | .id'
```

```
$ ed tools ls
ID          STATE       VERSION     SOURCE    USED BY
homebrew    installed   5.0.1       homebrew  homebrew, appMaintenance
herdr       missing                           herdr
quinjet     installed   0.0.86      homebrew  quinjet
gh          installed   2.104.0     homebrew  latex, codeStats, quinjet
git         installed   2.50.1      system    codeStats, bifrost
yt-dlp      installed   2026.10.26  edith     music, downloads
ffmpeg      installed   8.0.1       homebrew  music, studio, downloads
deno        missing                           music, downloads
gallery-dl  missing                           music, downloads
tectonic    missing                           latex
latexmk     detectOnly                        latex
ripgrep     installed   15.2.0      homebrew  beacon
sshfs       missing                           machines
```

## Where to go next

- [`ed tools`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
