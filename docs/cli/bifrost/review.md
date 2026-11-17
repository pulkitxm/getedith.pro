# `ed bifrost review`

Inspect large, old, duplicate, installer or empty files. This command never removes anything.

```sh
ed bifrost review ~/Downloads --minimum-mb 100 --json
ed bifrost review ~/Downloads --extension dmg --extension pkg --no-duplicates
ed bifrost review ~/Documents --minimum-mb 0 --older-than-days 90
ed bifrost review ~/Downloads --minimum-mb 0 --maximum-mb 0 --no-duplicates
ed bifrost review ~/Documents --exclude ~/Documents/Keep --maximum-entries 100000 --hash-budget-mb 5000
```

| Control | Default | Meaning |
| --- | --- | --- |
| `--minimum-mb` | 10 | Minimum logical size in decimal MB. |
| `--maximum-mb` | Unlimited | Maximum logical size, inclusive. Zero with a zero minimum finds empty files. |
| `--older-than-days` | 0 | Minimum age since modification. |
| `--extension` | All | File suffix, repeatable and case-insensitive. |
| `--exclude` | None | Additional excluded path, repeatable. Persistent protections also apply. |
| `--hidden` | Off | Include hidden files and folders. |
| `--no-duplicates` | Off | Skip content hashing. |
| `--maximum-entries` | 50000 | Entry cap, from 1 to 200000. Directories count toward the cap. |
| `--hash-budget-mb` | 2000 | Maximum content comparison budget, from 0 to 100000 MB. |
| `--json` | Off | Export items, scan controls, coverage and up to 20 error details. |

Full SHA-256 hashes identify exact duplicates among files matching the filters. Hard-link aliases count once. Partial scans and exhausted hashing budgets are reported explicitly. A size-filtered scan cannot find duplicate copies outside that filter.

Scans stay on one filesystem and skip application bundles, links and cloud-only entries. Logical size is the file length. Allocated bytes describe storage attributed to a file, not the exact space deletion would free on APFS.

Open Bifrost's Files tab to review and select results for a confirmed Trash move.

[Back to Bifrost](./README.md).

[All commands](../README.md).
