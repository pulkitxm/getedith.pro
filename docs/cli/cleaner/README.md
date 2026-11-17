# `ed cleaner`

Cleaner combines Cleanup, Disk Map and File review. It uses native filesystem APIs and the existing `ed` interface. No separate Rust program or background cleanup daemon is required.

| Command | Purpose |
| --- | --- |
| [`scan`](./scan.md) | Inspect cache and project categories. |
| [`categories`](./categories.md) | Show every rule, path and default selection. |
| [`clean`](./clean.md) | Preview or move an explicit selection to Trash. |
| [`drives`](./drives.md) | List available volumes. |
| `worktrees --root <folder>` | Inspect worktree size, age and git status. |
| [`map <folder> --json`](./map.md) | Export allocated and logical sizes, coverage and ranked entries. |
| [`review <folder> --json`](./review.md) | Find large, old and duplicate files and installers. |
| [`protect [path]`](./protect.md) | Add a persistent protection, or list existing protections. |
| `protect <path> --remove` | Remove a protection. |
| [`history --json`](./history.md) | List recorded Trash locations and restore identifiers. |
| [`restore <receipt-id> [--yes]`](./restore.md) | Preview a restore, then apply it without overwriting files. |

## File review

```sh
ed cleaner review ~/Downloads --minimum-mb 10 --older-than-days 30 --json
ed cleaner review ~/Documents --minimum-mb 0 --exclude ~/Documents/Keep
ed cleaner review ~/Downloads --extension dmg --extension pkg --no-duplicates
```

`--hidden` includes hidden files. Review scans stay on one filesystem and skip cloud-only entries, packages and symbolic links. By default, at most 50,000 entries are visited and 2 GB of content is hashed per scan. Adjust these limits with `--maximum-entries` and `--hash-budget-mb`. `--minimum-mb 0 --maximum-mb 0` finds empty files. The report explicitly identifies limited scans and read errors. Narrow the scope to investigate further.

Duplicate groups use full SHA-256 content hashes after matching logical size. Hard-link aliases count once. No files start selected. The File review screen can select duplicate copies while retaining one copy; deletion refuses a group without an unchanged remaining copy. Size and age filters also restrict duplicate comparison, so groups are relative to that scan.

## Removal and restoration

Protected paths apply across all Cleaner removal routes. Protecting a child also prevents removal of its containing folder. The filesystem identity is checked before moving a reviewed item. Symbolic-link parent replacements are rejected.

Trash history records at most 500 receipts; the screen offers search and pages of 50 and the CLI lists all retained receipts. Restore uses an exclusive filesystem rename and refuses an occupied original path. Missing or changed Trash items must be handled in Finder. Cleaner never empties Trash. Bytes moved are not bytes immediately freed, and APFS shared blocks and snapshots can reduce eventual recovery.

## Navigation

Enable Cleaner in Library and open its page. Cleanup offers categories and worktree controls. Disk Map offers treemap and rings, largest-item lists, search, size filtering and hidden-entry controls. Files offers review presets, sorting, file selection and report export. Restore offers persistent protected paths and Trash history.

[All commands](../README.md).
