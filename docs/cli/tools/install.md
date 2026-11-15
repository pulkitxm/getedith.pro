# `ed tools install`

Installs one tool, or reports where it already is.

Usage:

```
ed tools install <tool> [--json]
```

Arguments:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `<tool>` | a tool id from [`ed tools`](./README.md) | required | Which tool to install. |

Options:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--json` | flag | off | Emits one JSON object on stdout. |

The command waits until the tool has landed. A tool that is already found
anywhere Edith looks is reported and left alone. Otherwise Edith picks the
source from the tool's catalog entry:

- a verified GitHub release download into Edith's tools folder, for tools that
  prefer it (yt-dlp, Deno, Herdr, Tectonic) or when Homebrew is missing;
- Homebrew, when it is present and the tool has a formula;
- Homebrew first, then the formula, when the tool only comes from Homebrew and
  Homebrew is missing. Installer opens for Homebrew's signed package and the
  command continues once it finishes;
- the signed installer packages (Homebrew, sshfs), opened in Installer;
- Apple's Command Line Tools installer, for Git.

`--json` shape:

```json
{
  "id": "yt-dlp",
  "changed": true,
  "version": "2026.10.26",
  "path": "/Users/me/Library/Application Support/Edith/Tools/bin/yt-dlp",
  "method": "direct"
}
```

`changed` is false when the tool was already there. `method` is `direct`,
`homebrew` or `package` for what Edith installed and records, and `null` for a
tool that was already present or came from Apple's installer.

Examples:

```
ed tools install yt-dlp
ed tools install ffmpeg --json
ed tools install gh
```

```
$ ed tools install yt-dlp
installed yt-dlp 2026.10.26

$ ed tools install ffmpeg
ffmpeg is already installed at /opt/homebrew/bin/ffmpeg
```

Failures exit 1 with one sentence, and leave nothing staged:

```
$ ed tools install deno
error: The download did not match its published checksum.

$ ed tools install latexmk
error: Edith cannot install TeX Live. Edith finds it once it is installed.
```

## Where to go next

- [`ed tools`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
