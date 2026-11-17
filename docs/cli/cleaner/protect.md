# `ed cleaner protect`

List persistent protections or add a path that every Cleaner scanner and removal route must respect.

```sh
ed cleaner protect ~/Documents/Keep
ed cleaner protect --json
ed cleaner protect ~/Documents/Keep --remove
```

Protecting a folder excludes its descendants. Protecting any child also prevents removal of a containing folder. Paths resolve relative to the caller's working directory, with tilde expansion. Removing a protection allows future review; it never deletes anything.

The Restore tab exposes the same protected-path list.

[Back to Cleaner](./README.md).

[All commands](../README.md).
