# `ed cursors status`

[`ed cursors`](./README.md)

[The `ed` command line](../README.md)

```bash
ed cursors status [--json]
```

Reports the applied pack with its size and changed colours, whether macOS is drawing it right now (`live`), whether this macOS supports cursor themes, how much disk the encrypted pack list, card pages and downloaded packs use, and whether pack downloads are available. JSON output has `activePack`, `activePackName`, `recipe` (`base`, `size` and `colors`, or null), `live`, `supported`, `unsupportedReason`, `cacheBytes`, `generated` (the date of the pack list), `access` and `retryAfter`. `access` is `open`, `licenseRequired` (activate Edith, then try again), `packBudget` (the daily limit on new packs is reached) or `rateLimited` (the service asked Edith to slow down); `retryAfter` is the ISO 8601 time to try again, when there is one.
