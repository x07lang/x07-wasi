# x07-wasi

Canonical [X07](https://github.com/x07lang/x07) packages exporting `std.wasi.*` — WASI types, codecs, and (future) effectful APIs for x07 programs targeting WASM.

x07-wasi is designed for **100% agentic coding** — an AI coding agent uses these packages to build WASI-aware x07 programs entirely on its own using structured contracts and machine-readable outputs. No human needs to write X07 by hand.

## Prerequisites

The [X07 toolchain](https://github.com/x07lang/x07) must be installed before using x07-wasi. If you (or your agent) are new to X07, start with the **[Agent Quickstart](https://x07lang.org/docs/getting-started/agent-quickstart)** — it covers toolchain setup, project structure, and the workflow conventions an agent needs to be productive.

## Purpose

x07-wasi is the single canonical source for `std.wasi.*` modules (per the [package policy](https://github.com/x07lang/x07/blob/main/docs/project/package-policy.md)). It provides:

- **Types and codecs** for WASI 0.2 interfaces (available now)
- **Effectful APIs** via WASI capability imports with strict budget/policy enforcement (future — see Phase 8 in the [WASM roadmap](https://github.com/x07lang/x07-wasm-backend))

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
