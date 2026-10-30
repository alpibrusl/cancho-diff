# CLAUDE.md -- cancho-diff

This repository is written in **cancho**, and only in cancho. Before writing any program here read
[`AGENTS.md`](https://github.com/alpibrusl/cancho/blob/main/AGENTS.md) (`cancho agent-guidelines` prints it from the compiler).

* **The gate**, all passing, before anything is called done: `cancho fmt --check src tests`; `cancho check src/*.cho --std`;
  `cancho test` over the files in `tests/`; no `.cho` file over 2,000 lines.
* **Standard library only.** No other package is a dependency.
* **Narrow the body, never widen the row.** `cancho authority` is the review artefact; a change that widens it says so in its commit message.
* **No input may reach a panic.** Any bytes, any patch: a value on a named path, never a trap.
* **Python (or any other language) is for test oracles only**, never product logic.
* **Compiler pin.** `.cancho-rev` and `.github/workflows/ci.yml` name the same revision. Do not bump it without re-running the gate.
* The held-out audit is not in this repository and must not be added to it.
