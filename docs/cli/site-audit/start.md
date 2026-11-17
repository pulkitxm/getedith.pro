# `ed site-audit start`

[`ed site-audit`](./README.md)

[The `ed` command line](../README.md)

```bash
ed site-audit start <id> [--scores] [--no-scores] [--wait] [--json]
```

Queues an audit of the selected pages. It uses the saved page scores switch unless `--scores` or `--no-scores` is set. Without `--wait` the command returns once the run is queued. `--wait` blocks until the run finishes. At least one page has to be selected.
