# Bifrost Disk Map

Enable **Bifrost** in Library, open its page and choose **Disk Map**.

```sh
ed extensions enable bifrost
ed app reveal bifrost
ed bifrost map ~/Downloads --json
```

Choose a folder to measure it. Treemap and Rings show the largest immediate children, sized by allocated space. Click a folder to scan inside it, go back to the previous folder, or rescan. The engine owns the scan when switching tabs; Cancel stops it. Bifrost does not automatically start background scans.

Lists contain at most 200 entries. Largest files, directories and cleanup candidates use a 50 MB threshold. Search full paths, filter by displayed size, hide dot-named entries, and switch size ordering to name ordering. Filters operate on the bounded scan report. Drill into a folder to inspect more entries.

The page shows logical and allocated bytes, folders and elapsed time. Hard links count once. Symlinks are not traversed, scans stay on one volume, and cloud-only directories and protected paths are skipped. Coverage warnings report read errors and skipped entries. Protected paths are managed in the Restore tab and apply to every removal route.

Reveal in Finder before choosing Trash. The current preview and file identity are checked before moving an item. Restore recorded items in the Restore tab or with `ed bifrost history` and `ed bifrost restore`. Bifrost does not empty Trash. Allocated bytes are not guaranteed recoverable space because APFS clones, snapshots and open files can retain blocks.

See the [Bifrost CLI guide](cli/bifrost/README.md) and [research notes](bifrost-research.md).
