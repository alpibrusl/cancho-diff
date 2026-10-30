# cancho-diff

[![ci](https://github.com/alpibrusl/cancho-diff/actions/workflows/ci.yml/badge.svg)](https://github.com/alpibrusl/cancho-diff/actions/workflows/ci.yml)

A line diff and patch for [cancho](https://github.com/alpibrusl/cancho), with nothing but the standard library.

## Status

**First build, 2026-10-30: `src/diff.cho` (685 lines) passes its 24 tests and a held-out audit of 2019 cases.** The audit is not in this
repository (see below). It checks the three functions against GNU `diff` 3.12 and `patch`: shortest scripts, the real `patch` applying
our output, our `apply` on real `diff -u` output, hunk headers and merging, the no-newline marker, tampered patches, and inputs of
800 to 3000 lines. Not claimed: anything about inputs the audit does not generate, performance beyond those sizes, or a `diff` command
(the library only). How it was made, with its one human intervention, is in [`docs/provenance.md`](docs/provenance.md).

## What it is

Three pure functions over bytes, read as lines (`import diff;`):

* `diff.edit_count(heap, a, b)`: the length of the shortest edit script from `a` to `b`;
* `diff.unified(heap, a_name, b_name, a, b, context)`: a unified diff in the format GNU `diff -u` prints, with the hunk rules and the
  no-newline marker, as a `buffer.Buffer`;
* `diff.apply(heap, patch, a)`: apply such a diff exactly (no fuzz): `Ok(text)`, or `Err(1)` for a malformed patch and `Err(2)` for
  one that does not fit `a`.

It imports `std.result` and `std.buffer` only: no file, network, process or clock. It is meant to become the `diff` tool that
`cancho-tools` defers today (D15), as a thin command-line layer on the cancho-tools contract; that decision is the maintainer's and has
not been recorded.

## How it is being made

By [Cancho Code](https://github.com/alpibrusl/cancho-code) under [Forge](https://github.com/alpibrusl/cancho-forge), with a person
approving the brief and the result. The code in `src/` came from that build, not from a hand: the changes made after it are listed in `docs/provenance.md`. The brief, the held-out
audit that judges it and its oracle are deliberately **not** in this repository: a builder that can read its judge optimises for the
judge.

## Layout

* `src/diff.cho`: the package
* `tests/diff_test.cho`: tests written from the brief's worked examples (not by the builder)
* `docs/provenance.md`: how it was built and what a person changed
* `CLAUDE.md`: the rules for whoever writes in this repository

## Requirements

The **cancho** compiler at the revision in `.cancho-rev` (CI builds that revision). A package store records no hash of the `std` it was
published against, so the compiler revision is part of the contract.
