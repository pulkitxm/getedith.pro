# `ed tools remove`

Removes one tool Edith installed.

Usage:

```
ed tools remove <tool> [--yes] [--json]
```

Arguments:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `<tool>` | a tool id from [`ed tools`](./README.md) | required | Which tool to remove. |

Options:

| Name | Type / values | Default | What it does |
| --- | --- | --- | --- |
| `--yes` | flag | off | Applies the removal. Without it the command only previews. |
| `--json` | flag | off | Emits one JSON object on stdout. |

Only tools recorded in `Tools/installed.json` can be removed. A direct download
is deleted from Edith's tools folder, and a Homebrew install Edith made runs
`brew uninstall`. Tools you installed yourself, and tools that came from an
installer package, are refused with a one sentence reason.

Preview shape:

```json
{
  "action": "remove",
  "targets": ["yt-dlp"],
  "applied": false,
  "changed": false,
  "requiresConfirmation": true
}
```

Examples:

```
ed tools remove yt-dlp
ed tools remove yt-dlp --yes
```

```
$ ed tools remove ffmpeg --yes
error: Edith did not install FFmpeg, so it leaves it alone.
```

## Where to go next

- [`ed tools`](./README.md), the rest of this group
- [All `ed` commands](../README.md)
