# `ed app-updates ignore`

Ignores one available update version.

[`ed app-updates`](./README.md)

Usage:

```
ed app-updates ignore <id> --available <version> [--json]
```

This writes the ignored-version policy the update list uses. A newer version of the same item still appears.

Examples:

```
ed app-updates ignore firefox --available 120.0
ed app-updates ignore firefox --available 120.0 --json
```

See also:

- [`ed app-updates snooze`](./snooze.md)
- [`ed app-updates`](./README.md)
- [`ed`](../README.md)
