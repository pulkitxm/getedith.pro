# `ed flags`

`ed flags` shows the feature flags this Mac uses: which extensions, theme
colors and app features the server has turned on for it, and whether this Mac
is in the beta. Edith checks a hash of its flags with every license heartbeat
and fetches the full set only when the hash changes. See
`docs/feature-flags.md` in the repository for how flags are evaluated and edited.

`ed flags` with nothing after it runs `ed flags ls`, and `ed flags list` is the
same command. Every verb runs in the Edith app.

## At a glance

| Command | What it does |
| --- | --- |
| `ed flags ls [--group G] [--json]` | Lists every flag with its value for this Mac. `G` is `extensions`, `themes`, `features` or `access`. |
| `ed flags get <key> [--json]` | Shows one flag. |
| `ed flags refresh [--force] [--json]` | Checks the hash now and fetches the flags when it changed, or always with `--force`. |
| `ed flags beta [on\|off] [--json]` | Shows or changes whether this Mac is in the beta. |

`VALUE` is the value for this Mac's audience: the beta value when the Mac is in
the beta, the general value otherwise. `DETAIL` shows the stage of an extension
(`stable`, `beta` or `disabled`) or both audience values of any other flag. A
flag the app has never received is on.

`--json` shape of `ls`:

```json
{
  "audience": "general",
  "source": "server",
  "hash": "3f1c...",
  "revision": 42,
  "fetchedAt": "2026-11-18T09:12:00Z",
  "checkedAt": "2026-11-18T09:20:00Z",
  "flags": [
    { "key": "extension.hinge", "enabled": false, "general": false, "beta": true, "stage": "beta" }
  ]
}
```

`source` is `server` once a set was fetched and `defaults` before that.
Development builds that do not enforce licensing never fetch flags.

Examples:

```
ed flags ls --group extensions
ed flags get feature.mcp
ed flags refresh
ed flags beta on
```

## Exit codes

| Code | When this group produces it |
| --- | --- |
| 0 | The flags printed or the setting changed. |
| 2 | An unknown verb, flag or group. |
| 1 | `refresh` could not reach the server, or `get` named a flag the server does not have. |

## Where to go next

- [`ed extensions`](../extensions/README.md), which shows each extension's state
- [All `ed` commands](../README.md)
