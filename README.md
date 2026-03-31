# x07-wasi

## Agent Entrypoint

Start here: https://x07lang.org/docs/getting-started/agent-quickstart

`x07-wasi` is the canonical public home for `std.wasi.*` in the [X07](https://github.com/x07lang/x07) ecosystem. It exists to hold the WASI-facing packages, contracts, and release line that x07 programs can depend on when targeting WebAssembly and WASI hosts.

The vision is to give x07 one clear, official place for WASI integration instead of scattering WASI support across unrelated repos. End users should be able to look at this repo and know where the `std.wasi.*` story lives.

x07-wasi is designed for **100% agentic coding**. Coding agents need a stable namespace, a single source of truth, and clear package ownership. This repo provides that boundary.

## What is in this repo today

Today this repo is intentionally small. Its current job is to reserve and document the canonical `std.wasi.*` namespace and the release boundary for future WASI packages. As the WASI surface is published, this repo is where the official packages and related documentation will live.

## How it fits into the x07 ecosystem

`x07-wasi` is part of the WASM line of the ecosystem:

- **`x07`** is the language and core toolchain.
- **`x07-wasm-backend`** builds and runs x07 programs as WASM modules, components, web apps, and device bundles.
- **`x07-wasi`** owns the standard-library namespace for WASI-specific types and APIs used by those builds.

That split keeps responsibilities clear: `x07-wasm-backend` owns the build and runtime tooling, while `x07-wasi` owns the public package namespace that x07 programs import.

## Prerequisites

The [X07 toolchain](https://github.com/x07lang/x07) must be installed before using x07-wasi. If you (or your agent) are new to X07, start with the **[Agent Quickstart](https://x07lang.org/docs/getting-started/agent-quickstart)** — it covers toolchain setup, project structure, and the workflow conventions an agent needs to be productive.

## Practical usage

You will care about `x07-wasi` when you are:

- building x07 programs that need to target standard WASI hosts
- looking for the official `std.wasi.*` package line instead of a third-party namespace
- keeping WASI-facing code aligned with the rest of the x07 WASM toolchain

In day-to-day work, most users will meet this repo through the wider x07 flow:

1. write the program with `x07`
2. build or run it with `x07-wasm`
3. depend on `std.wasi.*` packages owned by this repo when the program needs WASI contracts

## Purpose

x07-wasi is the single canonical source for `std.wasi.*` modules (per the [package policy](https://github.com/x07lang/x07/blob/main/docs/project/package-policy.md)). It provides:

- **Types and codecs** for WASI 0.2 interfaces (available now)
- **Effectful APIs** via WASI capability imports with strict budget/policy enforcement (future — see Phase 8 in the [WASM roadmap](https://github.com/x07lang/x07-wasm-backend))

## Install and use

There is no standalone end-user binary in this repo. The normal way to use it is through the X07 toolchain and package workflows.

As published packages appear, the end-user flow will be:

```bash
x07 pkg add <std.wasi package>@<version> --sync
```

Then build and run the project with the normal x07 WASM tooling from `x07-wasm-backend`.

## Security notes

WASI is an interface contract; the security boundary comes from the chosen WASM runtime and the host capabilities you expose.

If you need to execute untrusted WASM/WASI code, use a hardened runtime (for example Wasmtime, as used by `x07-wasm`) with a deny-by-default capability model and resource limits. Node’s `node:wasi` APIs are not intended to be a security sandbox — do not rely on them to run untrusted code.

## Namespace rules

Only this repo exports `std.wasi.*`. Platform-specific modules must use a non-`std.*` namespace.

## Links

- [X07 Agent Quickstart](https://x07lang.org/docs/getting-started/agent-quickstart) — start here
- [X07 toolchain](https://github.com/x07lang/x07)
- [X07 website](https://x07lang.org)
- [WASM build tooling](https://github.com/x07lang/x07-wasm-backend)

## License

Dual-licensed under [Apache 2.0](LICENSE-APACHE) and [MIT](LICENSE).
