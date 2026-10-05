# contract-bus

The weft plane harness: a command in, reply bytes out, over iceoryx2 shared memory with no daemon and no copy.

## What it is for

It is the contract a transport layer and an interactor compose against, so every caller reaches an interactor through the same envelope. Every plane and edge links `weft::harness` and none of them links iceoryx2: the C ABI is named in a signature file and turned into a dlsym dispatch table, so a plane builds without the library and a missing bus fails at start-up with a message rather than at link time. `docs/` holds the design and the plan.

## Build

```sh
cmake -B build
cmake --build build
```

iceoryx2 is built separately and loaded at run time; nothing here vendors it.

## Licence

Apache-2.0; see `LICENSE`.
