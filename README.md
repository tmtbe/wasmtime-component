## Steps to repro

Build the lib:

```
cargo build --target wasm32-wasi
```

Download the necessary adapter file from [here](https://github.com/bytecodealliance/wasmtime/releases/tag/v14.0.4), rename it to `wasi_snapshot_preview1.wasm`, and place it in the root of the repository. Be sure to download the `*.reactor.wasm` variant. 

Create the WASM component:

```
wasm-tools component new target/wasm32-wasi/debug/wasm_components.wasm -o component.wasm --adapt ./wasi_snapshot_preview1.wasm
```

Run the example:

```
cargo run --example hello
```

You should run into the following error when instantating the module:

```
Error: import `wasi:io/streams@0.2.0-rc-2023-10-18` has the wrong type

Caused by:
    0: instance export `output-stream` has the wrong type
    1: expected resource found nothing
```
