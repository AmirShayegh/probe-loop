# The Probe Loop (TLDR)

> Tests verify contracts. Probes verify reality.

After the tests are green and the architecture is settled, the question becomes whether the system actually works against the real runtime. The probe loop is the answer.

**The loop, five stages:**

1. **Probe** the real production path
2. **Verify** the actual output, not the status code
3. **Discover** where report and reality diverge
4. **Fix** the root cause (rarely the layer that surfaced the symptom)
5. **Lock** the probe as a regression gate

**The bugs it catches** (the ones that survive contract testing):

- Silent no-ops: output equals input, status says success
- Environment mismatches: correct against spec, broken against runtime
- Swallowed errors: failure path drops the diagnostic or returns truncated output
- Hardcoded parameters: works for one case, silently wrong for the rest
- Cross-layer trust violations: each layer assumes the other handled it
- Destructive edge cases: safe in the common case, destroys data in the corner

**Why now:** the loop only became affordable when an agent could hold the codebase, the failure trace, and the regression-test draft inside a single context. The substrate change is the news. The practice is old.

**When to run one:**

- Tests are green but no one has inspected the output
- A feature crosses provider, runtime, file, stream, or network boundaries
- Fixtures represent the API contract, not the live runtime
- An agent generated code that has not been exercised through the real path
