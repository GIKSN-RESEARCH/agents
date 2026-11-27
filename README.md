# agents

A durable agent framework in Rust, with Go to follow. Built in public. Part of [Open Build AI](https://www.giksn.com) by GIKSN Research.

> **Status: research phase.** There is no working framework yet. This repository holds the research, the designs and the plan. Code will land as each design is accepted.

## What it will be

- **Core types:** messages, models, tools and structured output, with tool schemas generated from Rust types.
- **A durable graph runtime:** supersteps, typed state with reducers, a checkpoint after every step, and interrupts that pause a run until a human answers.
- **A ready-made agent** with middleware hooks around every model and tool call.
- **Streaming:** state values, updates, model messages, custom events, checkpoints, tasks and debug.
- **An agent server:** assistants, threads, runs and streams over HTTP, published as an OpenAPI spec.
- **A Go implementation** built from the same spec and checked by the same conformance suite.

None of the work in this repository needs a GPU.

## Layout

| Path | Contents |
| --- | --- |
| `research/` | Research notes and experiments |
| `rfcs/` | Design proposals and decisions |
| `crates/` | The framework, one crate per concern. Empty until designs are accepted |
| `spec/` | The planned language-neutral spec and conformance fixtures |
| `go/` | The planned Go implementation |
| `docs/ROADMAP.md` | The planned order of work |

## Contributing

Read [`CONTRIBUTING.md`](CONTRIBUTING.md) and the pinned **Start here** issue. None of the work in this repository needs a GPU.

## Licence

Dual licensed under MIT or Apache-2.0, at your option.
