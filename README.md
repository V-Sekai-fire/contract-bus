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

## Run

The command and reply proof sends commands from one process and reads replies in the other:

```sh
export WEFT_ICEORYX2_PATH=/path/to/libiceoryx2_ffi_c.so  # .dylib on macOS, .dll on Windows
./build/weft-harness-command_subscriber 8 &
./build/weft-harness-command_publisher 8
```

`WEFT_ICEORYX2_PATH` names the iceoryx2 C library, and is optional where that library is on the loader's search path.

## Licence

Apache-2.0; see `LICENSE`.
