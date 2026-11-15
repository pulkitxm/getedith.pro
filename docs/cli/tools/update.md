# `ed tools update`

Updates one tool.

Usage:

```
ed tools update <tool> [--json]
```

Arguments:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `<tool>` | a tool id from [`ed tools`](./README.md) | required | Which tool to update. |

Options:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--json` | flag | off | Emits one JSON object on stdout, the same shape as `install`. |

What happens depends on how the tool got there:

| Installed by | Update |
| --- | --- |
| Edith, direct download | Downloads and verifies the latest release when its tag differs from the recorded version, then replaces the binary. |
| Edith, Homebrew | `brew upgrade <formula>`. |
| You, with Homebrew | `brew upgrade <formula>`, for tools that have a formula. |
| An installer package | Refused: update it with its own updater. |
| Anything else | Refused: Edith leaves tools it did not install alone. |

Examples:

```
ed tools update yt-dlp
ed tools update ffmpeg --json
```

```
$ ed tools update yt-dlp
updated yt-dlp 2026.11.01

$ ed tools update yt-dlp
yt-dlp is up to date at /Users/me/Library/Application Support/Edith/Tools/bin/yt-dlp
```

## Where to go next

- [`ed tools`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
