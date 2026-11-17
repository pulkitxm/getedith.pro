# `ed bifrost protect`

List persistent protections or add a path that every Bifrost scanner and removal route must respect.

```sh
ed bifrost protect ~/Documents/Keep
ed bifrost protect --json
ed bifrost protect ~/Documents/Keep --remove
```

Protecting a folder excludes its descendants. Protecting any child also prevents removal of a containing folder. Paths resolve relative to the caller's working directory, with tilde expansion. Removing a protection allows future review; it never deletes anything.

The Restore tab exposes the same protected-path list.

[Back to Bifrost](./README.md).

[All commands](../README.md).
