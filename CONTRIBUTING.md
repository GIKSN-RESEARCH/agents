# Contributing

The [org-wide contribution rules](https://github.com/GIKSN-RESEARCH/.github/blob/main/CONTRIBUTING.md) apply here.

## Where things go

| Path | Contents |
| --- | --- |
| `research/` | Research notes and experiments |
| `rfcs/` | Design proposals and decisions |
| `crates/` | The framework, one crate per concern. Empty until designs are accepted |
| `spec/` | The planned language-neutral spec and conformance fixtures |
| `go/` | The planned Go implementation |
| `docs/ROADMAP.md` | The planned order of work |

## Commands

```bash
cargo fmt --all
cargo clippy --workspace --all-targets -- -D warnings
cargo test --workspace
```

## Unsafe code

`unsafe_code` is denied in every crate. This repository has no GPU feature or GPU requirement.

## Correctness first

Changes to public types, checkpoint records and stream events will need an accepted RFC. Tests will check serialization round trips, reducer behavior and checkpoint recovery as those components are built.

## Research experiments

Experiments will usually run on a CPU. Record the OS, toolchain and any model API used in `env.txt`. See [the research guide](research/README.md).
