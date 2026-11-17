# `ed cleaner scan`

Measure how much disk space you can reclaim from caches and generated project artifacts without changing files. This is the default subcommand.

```sh
ed cleaner scan --json
ed cleaner scan --category chromeCache
ed cleaner scan --root ~/code --category nodeModules --older-than 2w
```

`--category` selects an exact identifier from `ed cleaner categories`. `--root` adds project discovery and may be repeated. `--older-than` filters by modification age, with units `m`, `h`, `d`, `w`, `mo` or `y`. `--json` includes the complete category and item list with allocated sizes and paths.

Persistent path protections apply to discovery and removal. Cache children, including hidden children, are individually listed. Cache content dates reflect the newest measured modification. Project scanning uses project markers to distinguish generated artifacts from similarly named ordinary folders. A scan does not change the filesystem and does not authorize a later cleanup.

For general files, duplicates and installers use `ed cleaner review <folder>`. For filesystem allocation and largest-folder views use `ed cleaner map <folder>`.

[Cleaner](./README.md) · [All commands](../README.md).
