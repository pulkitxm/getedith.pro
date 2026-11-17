# `ed app-updates updates`

[`ed app-updates`](./README.md)

[The `ed` command line](../README.md)

```bash
ed app-updates updates [--json]
```

Discovers Homebrew cask and formula, Mac App Store (apps with an App Store receipt, looked up in Apple's public catalog), Sparkle, and standard HTTPS app-feed updates. Human output shows versions, source, and confidence. JSON includes release information, freshness, application identity, `action` (`install` or `openUpdater`) and `update` (`homebrew`, `appStore` or `openApplication`). Discovery never installs anything.
