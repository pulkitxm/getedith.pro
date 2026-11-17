# `ed app-updates scan`

[`ed app-updates`](./README.md)

[The `ed` command line](../README.md)

```bash
ed app-updates scan /Applications/Example.app [--json]
```

Builds a read-only removal plan. The plan contains the app bundle and existing user Library entries whose filename is the app's exact verified bundle identifier, plus the standard suffix used by Preferences and Saved Application State.

The command rejects protected, nested, symlinked, missing, or malformed applications. Run it again if an app changed after the previous scan.
