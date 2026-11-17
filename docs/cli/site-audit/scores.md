# `ed site-audit scores`

[`ed site-audit`](./README.md)

[The `ed` command line](../README.md)

```bash
ed site-audit scores <id> <on|off> [--json]
```

Writes the page scores switch used by the next audit. It does not start one. `on` scores each page for performance, accessibility, best practices and SEO. `off` records metadata only. `ed site-audit start --scores` or `--no-scores` overrides this for a single run.

Page scores are measured inside Edith: each page loads in a private, offscreen web view that records Navigation Timing, first and largest contentful paint, layout shifts and main-thread blocking, and runs the bundled axe-core accessibility checker. Nothing needs to be installed.
