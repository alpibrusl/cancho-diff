# cancho-diff

[![ci](https://github.com/alpibrusl/cancho-diff/actions/workflows/ci.yml/badge.svg)](https://github.com/alpibrusl/cancho-diff/actions/workflows/ci.yml)

A line diff and patch for [cancho](https://github.com/alpibrusl/cancho), with nothing but the standard library.

## Status

**Empty. Nothing is built, nothing is measured.** This repository holds a skeleton (licence, CI, layout) and nothing else.

## What it will be

Three pure functions over bytes, read as lines:

* `edit_count(heap, a, b)`: the length of the shortest edit script from `a` to `b`;
* `unified(heap, a_name, b_name, a, b, context)`: a unified diff in the format GNU `diff -u` prints, with the hunk rules and the
  no-newline marker;
* `apply(heap, patch, a)`: apply such a diff exactly (no fuzz), or answer a documented error number.

No files, no network, no process, no clock: the package's authority report is meant to show `heap` and nothing else. It is meant to
become the `diff` tool that `cancho-tools` defers today (D15), as a thin command-line layer on the cancho-tools contract; that
decision is the maintainer's and has not been recorded.

## How it is being made

By [Cancho Code](https://github.com/alpibrusl/cancho-code) under [Forge](https://github.com/alpibrusl/cancho-forge), with a person
approving the brief and the result. The code in `src/` will come from that build, not be written by hand. The brief, the held-out
audit that judges it and its oracle are deliberately **not** in this repository: a builder that can read its judge optimises for the
judge.

## Layout

* `src/`: the package (empty)
* `tests/`: its tests (empty)
* `docs/`: design and measurements (empty)
* `CLAUDE.md`: the rules for whoever writes in this repository

## Requirements

The **cancho** compiler at the revision in `.cancho-rev` (CI builds that revision). A package store records no hash of the `std` it was
published against, so the compiler revision is part of the contract.
