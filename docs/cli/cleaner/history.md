# `ed cleaner history`

List receipts for files moved to Trash by Cleaner, including their identifiers and original paths.

```sh
ed cleaner history
ed cleaner history --json
```

Cleaner retains at most 500 receipts. The app offers path search and pages of 50 receipts. A receipt does not guarantee the item still exists in Trash. Emptying Trash or changing an item may prevent restoration.

Use the receipt identifier with [`restore`](./restore.md).

[Back to Cleaner](./README.md).

[All commands](../README.md).
