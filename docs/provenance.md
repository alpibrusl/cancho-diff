# Provenance of src/diff.cho

Built on 2026-10-30 by Cancho Code (`cancho-build`, plan agent and unit agent: Claude Haiku 5.5) under Forge's company layer, from a
brief and a contract of three signatures that a person wrote. A held-out audit the builder never saw judged it; Forge ran that audit
itself and accepted the step. The brief, the contract and the audit are not in this repository.

| | |
|---|---|
| Compiler | cancho f4ead824f33b291a0ad7620a34a0c1346a7abe4f |
| Planner | cancho-code with the `brief-heap` rule of alpibrusl/cancho-code#103 |
| Runs | 2 (the first ended `stuck`, see below) |
| Tokens (both runs) | about 82k in, 221k out, 258k cache read; priced under 1 USD (not priced exactly) |
| Audit | 2019 of 2019 |

## What a person changed

1. **One expected string in the model's plan.** The plan's case `test_script_7` expected `" -+"` for the pair `a,b,c` and `a,B,c`; the
   merged script is `" -+ "`. No correct implementation could pass it, and the first run ended `stuck` on that unit. The operator
   edited that string and approved a retry; the units already verified were kept.
2. **After the build, for use as a library:** `module diff;` added after `edition 7;`, `pub` added to the three public functions
   (`edit_count`, `unified`, `apply`), and the file formatted with `cancho fmt`. Run through the audit again with the `module` line
   removed: 2019 of 2019.
3. **The tests in `tests/diff_test.cho` were written by a person from the brief's worked examples**, not by the builder; the builder's
   own tests (one set per unit, testing private helpers) are not included.

## Not shown

The audit generates its inputs from a fixed seed. Nothing here says how the library behaves on kinds of input the audit does not
generate, nor how fast it is beyond 3000 lines.
