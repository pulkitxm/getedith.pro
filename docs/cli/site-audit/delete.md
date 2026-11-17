# `ed site-audit delete`

[`ed site-audit`](./README.md)

[The `ed` command line](../README.md)

```bash
ed site-audit delete <id> [--yes] [--json]
```

Previews the project that would be removed. `--yes` deletes the project, its page assets, and its page selection. Without `--yes` nothing is removed. `rm` is an alias. The agent refuses the delete while an audit is running.
