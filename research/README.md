# Research

Research will produce three kinds of artefact:

- Notes in `notes/` will survey sources or analyse a question that informs a design decision. Start with the [note template](notes/0000-template.md).
- Experiments in `experiments/` will record a question, a method and reproducible measurements. Start with the [experiment template](experiments/0000-template/README.md). Each completed experiment will include its script or notebook, raw `results.json` and `env.txt`.
- RFCs in [`../rfcs/`](../rfcs/) will propose designs for review. Use the [RFC template](../rfcs/0000-template.md) and the process in `CONTRIBUTING.md`.

Each series uses four-digit numbers. Choose the next free number in that series and never reuse a number, including after a rejection. The `0000` entries are templates.

Experiments in this repository will usually be CPU-only. `env.txt` should still record the OS, toolchain and any model API used.
