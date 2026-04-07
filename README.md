# x07-wasi

Canonical home for `std.wasi.*` in the X07 ecosystem.

This repo owns the public WASI-facing namespace for X07 packages. It exists so users and tools have one clear place to look for the official WASI contract line instead of guessing across unrelated repos.

**Start here:** [`x07lang/x07-wasm-backend`](https://github.com/x07lang/x07-wasm-backend) · [`x07lang/x07`](https://github.com/x07lang/x07)

## What This Repo Is Today

Today `x07-wasi` is intentionally small. Its current role is to hold and document the canonical `std.wasi.*` package boundary and release line as the WASI surface grows.

## When You Care About This Repo

You will usually care about `x07-wasi` when you are:

- targeting standard WASI hosts
- looking for official `std.wasi.*` packages
- trying to understand where WASI-specific contracts belong in the ecosystem

Most users will meet it through the broader flow:

1. write code with `x07`
2. build or run it with `x07-wasm`
3. depend on `std.wasi.*` packages from this repo when WASI contracts are needed

## Boundary

- `x07-wasi` owns the `std.wasi.*` namespace
- `x07-wasm-backend` owns the WASM and WASI build/runtime tooling

There is no standalone end-user binary in this repo. The normal consumer path is through X07 package workflows such as:

```sh
x07 pkg add <std.wasi package>@<version> --sync
```

## Security Notes

WASI is an interface contract, not a sandbox by itself. The real security boundary comes from the chosen runtime and the capabilities you expose to it. If you need to run untrusted code, use a hardened runtime with deny-by-default capabilities and resource limits.

## License

Dual-licensed under [Apache 2.0](LICENSE-APACHE) and [MIT](LICENSE).
