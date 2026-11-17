# `ed app-updates`

`ed app-updates` is the command-line surface for App Updates. It discovers updates across supported sources, runs reviewed batches, verifies and installs single-app disk images, previews exact bundle-identifier support files, and moves confirmed selections to the Trash.

[The `ed` command line](../README.md)

| Command | What it does |
| --- | --- |
| [`ed app-updates inventory`](./inventory.md) | Lists installed applications and optional Homebrew updates. |
| [`ed app-updates scan`](./scan.md) | Prints the application and exact support files Edith can review. |
| [`ed app-updates remove`](./remove.md) | Previews the removal selection, or moves it with `--yes`. |
| [`ed app-updates install`](./install.md) | Verifies and previews a single-app disk image, or installs it with `--yes`. |
| [`ed app-updates updates`](./updates.md) | Discovers the unified update inventory. |
| [`ed app-updates update`](./update.md) | Previews a selected update batch, or runs it with `--yes`. |
| [`ed app-updates history`](./history.md) | Shows persisted per-item update results. |
| [`ed app-updates backup-updates`](./backup-updates.md) | Copies update policy and history to a new file. |
| [`ed app-updates ignore`](./ignore.md) | Ignores one available update version. |
| [`ed app-updates snooze`](./snooze.md) | Hides one update for a duration. |
| [`ed app-updates exclude`](./exclude.md) | Stops offering updates for a bundle identifier. |
| [`ed app-updates reset`](./reset.md) | Clears ignore, snooze and exclude policy. |

Commands run locally and do not require Edith to be open. `inventory`, `updates`, `history`, and `scan` are read-only. `update`, `remove`, and `install` require `--yes` before applying their reviewed plan.

The App Updates extension settings explain the same supported paths and safety rules in the app.
