# `ed seo start`

[`ed seo`](./README.md)

[The `ed` command line](../README.md)

```bash
ed seo start <id> [--scores] [--no-scores] [--wait] [--json]
```

Queues an audit of the selected pages. It uses the saved page scores switch unless `--scores` or `--no-scores` is set. Without `--wait` the command returns once the run is queued. `--wait` blocks until the run finishes. At least one page has to be selected.
