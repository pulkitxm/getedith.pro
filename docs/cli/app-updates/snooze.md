# `ed app-updates snooze`

Hides one update until a duration from now.

[`ed app-updates`](./README.md)

Usage:

```
ed app-updates snooze <id> --for <duration> [--json]
```

Durations look like `12h` or `7d`.

Examples:

```
ed app-updates snooze firefox --for 7d
ed app-updates snooze firefox --for 7d --json
```

See also:

- [`ed app-updates ignore`](./ignore.md)
- [`ed app-updates`](./README.md)
- [`ed`](../README.md)
