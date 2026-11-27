# Roadmap

All phases below are planned. There is no working framework yet.

## 1. Research and spec

We will survey state and persistence designs and draft shared schemas and fixtures.

Exit criterion: Reviewed notes and draft message, checkpoint and API specs will define the first implementation targets.

## 2. Core types and the `#[tool]` macro

We will implement messages, model and tool traits, structured output and schema generation.

Exit criterion: Serialization fixtures and macro compile-pass and compile-fail tests will pass.

## 3. Graph runtime with in-memory checkpoints

We will implement nodes, edges, reducers and supersteps with an in-memory saver.

Exit criterion: Deterministic tests will verify fan-out merges and resume from each superstep checkpoint.

## 4. SQLite and Postgres checkpoints, interrupts

We will add persistent savers and pause-and-resume behavior.

Exit criterion: The same run will recover after a process restart on each saver and resume an interrupted step.

## 5. Agent and middleware

We will add the tool-calling agent and its six middleware hooks.

Exit criterion: Scripted model and tool tests will verify hook order, tool selection and termination.

## 6. Server and streaming

We will implement assistants, threads, runs and streams over HTTP.

Exit criterion: API tests will match the OpenAPI spec, and SSE fixtures will verify every accepted stream mode.

## 7. Tracing

We will add OpenTelemetry spans for model calls, tool calls and graph steps.

Exit criterion: A test exporter will capture spans with correct parent relationships and error fields for a complete run.

## 8. Go implementation against the conformance suite

We will build the Go implementation from the shared spec.

Exit criterion: Rust and Go will pass the same conformance suite without implementation-specific expected outputs.
