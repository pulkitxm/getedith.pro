# `ed cleaner categories`

List supported cleanup rules, their filesystem locations, explanations and default selections.

```sh
ed cleaner categories
ed cleaner categories --json
```

The catalogue includes Xcode, language and package-manager caches, browser and application caches, crash reports, archives and device backups. Additional project rules are discovered under explicit roots. Category identifiers are case-sensitive.

Browser caches, application caches, device backups and crash reports added with Cleaner start unchecked. Quit the owning application before removing caches. Device backups and release archives contain valuable data and require deliberate selection. JSON includes `category`, `name`, `detail`, `paths` and `onByDefault` for each catalogue entry.

[Cleaner](./README.md) · [All commands](../README.md).
