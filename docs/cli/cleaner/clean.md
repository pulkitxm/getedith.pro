# `ed cleaner clean`

Clean developer caches, browser caches and generated project artifacts. Preview selected cleanup candidates, then add `--yes` to move them to Trash.

```sh
ed cleaner clean --category npm --json
ed cleaner clean --category npm --exclude ~/.npm/_cacache/keep --yes
ed cleaner clean --root ~/code --path ~/code/example/node_modules --yes
ed cleaner clean --category iosBackups --include-review-required
```

| Option | Effect |
| --- | --- |
| `--category <id>` | Limit discovery to a rule listed by `categories`. |
| `--root <folder>` | Also inspect project artifacts; repeat for several roots. |
| `--path <path>` | Select only these exact discovered items; repeat for several items. Unknown or protected paths are rejected. |
| `--exclude <path>` | Protect a path, its contents and containing deletion candidates for this run. |
| `--include-review-required` | Explicitly include unchecked categories such as archives, backups and project artifacts. |
| `--older-than <duration>` | Filter by content age, for example `2d`, `1w`, `3mo`. |
| `--include-dirty` | Allow worktrees with uncommitted changes. Unpushed and locked worktrees remain protected. |
| `--yes` | Apply the previewed selection rules. Omit for a read-only preview. |
| `--json` | Emit selected paths, byte estimates and per-path failures. |

Without `--path` or `--include-review-required`, only default-selected rules are eligible. Each invocation discovers current candidates again. Use exact `--path` selections when the set must not broaden, or use the screen's scan-bound confirmation. The scan's file identity must still match immediately before moving it.

The applied JSON reports `movedBytes`, `paths`, `failures`, `items`, `plannedBytes` and `applied`. `applied` means execution was requested, not that every move succeeded. Failed paths remain in place. Disk space remains occupied until Trash is emptied separately.

[Cleaner](./README.md) · [All commands](../README.md).
