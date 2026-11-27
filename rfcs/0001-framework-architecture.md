# RFC 0001: Framework architecture

- Status: Draft
- Author: @SiddharthManjul
- Created: 2026-11-27
- Discussion: (link to pull request)
- Decision: (filled in by a maintainer)

## Summary

The framework will separate core types, graph execution, persistence and serving. Rust will come first. A Go implementation will later use the same language-neutral spec and conformance fixtures.

| Crate | Package | Planned responsibility |
| --- | --- | --- |
| `core` | `giksn-agents-core` | Messages, content blocks, the model trait, the tool trait, structured output and stream events |
| `macros` | `giksn-agents-macros` | The `#[tool]` and `#[derive(State)]` procedural macros |
| `graph` | `giksn-agents-graph` | Graph runtime: nodes, edges, branches, fan-out, supersteps, interrupts and subgraphs |
| `checkpoint` | `giksn-agents-checkpoint` | The checkpoint saver trait and record format |
| `agent` | `giksn-agents` | A ready-made tool-calling agent and its middleware |
| `server` | `giksn-agents-server` | HTTP server for assistants, threads, runs and streams |
| `trace` | `giksn-agents-trace` | OpenTelemetry spans for model calls, tool calls and graph steps |

## Motivation

The design will define how state updates, durable execution and streaming fit together before those interfaces are implemented. Shared schemas and fixtures will keep future Rust and Go implementations compatible.

## Design

### Layers and crates

`core` will define shared types. `macros` will generate tools and state helpers. `graph` will execute work using `checkpoint` storage. `agent` will compose model and tool calls. `server` will expose that execution over HTTP. `trace` will provide telemetry across those layers.

### Core types

A message enum will carry content blocks for text, images, tool calls and tool results. A model trait will expose invoke and stream operations. A tool trait will expose a name, description, input schema and invocation. Structured output and stream events will use serializable types.

### Tool macros

`#[tool]` will generate a tool name, description and JSON schema from a function signature and its Rust types. Compile-time errors will point to unsupported inputs. `#[derive(State)]` will generate the state helpers.

### Graph state and reducers

Graph state will be a struct with a reducer for each field. The state macro will generate a partial-update type so a node will update only the fields it owns. Reducers will combine updates from parallel nodes in a defined order.

### Supersteps and checkpoints

The runtime will use Pregel-style supersteps. It will collect node updates, apply reducers and write a checkpoint after each superstep. Checkpoints will be keyed by thread id and will record enough scheduling state to resume the next step.

### Interrupts and resume

An interrupt will persist a pending input request and pause the run. Resume will supply the human response and continue from the saved checkpoint. Tests will check repeated resume attempts and recovery after process restarts.

### Middleware

Middleware will provide six hooks: before the agent, after the agent, before each model call, after each model call, a wrapper around model calls and a wrapper around tool calls. The wrappers will control whether and how the underlying operation runs.

### Stream modes

One enum will describe state values, updates, model messages, custom events, checkpoints, tasks and debug events. Each mode will have a documented payload and ordering contract.

### Server resources

The HTTP API will expose assistants, threads, runs and streams. An OpenAPI document in `spec/` will define the endpoints, request bodies and responses before implementation.

### Checkpoint schema versioning

Every checkpoint record will contain a schema version. Readers will reject unsupported versions explicitly. A research note and follow-up RFC will define migrations and compatibility guarantees before a persistent format is accepted.

### Go plan

The Go implementation will follow the schemas and behavior in `spec/`. Both implementations will pass the same conformance suite. The Go work will start after the spec and fixtures have enough coverage to test compatibility.

## Alternatives

The research phase will compare reducer designs, schema-generation choices and checkpoint formats. Those notes will inform follow-up RFCs rather than fix those choices here without measurements.

## How it will be verified

| Layer | Verification |
| --- | --- |
| Core types | Serialization round trips and shared message fixtures will check JSON compatibility |
| Macros | Compile-pass and compile-fail cases will check generated schemas and diagnostics |
| Graph runtime | Deterministic tests will check reducer merges, superstep boundaries and fan-out |
| Checkpoints | Restart tests will resume from committed checkpoints without losing recorded updates |
| Interrupts | Tests will pause, persist and resume a run with a human response |
| Agent and middleware | Scripted model and tool implementations will check hook order and tool-call behavior |
| Server and streams | API and SSE tests will follow the OpenAPI document and event fixtures |
| Rust and Go | Both implementations will pass the same conformance fixtures |

## Open questions

- How deep will nested reducers go?
- What compile-time cost will the macros add?
- How will checkpoint schema migrations work?
- What will the stream event wire format be?
