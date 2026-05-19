# Probe Loop

A Claude Code plugin marketplace for verifying software against the real runtime, not just against its own contracts.

> Tests verify contracts. Probes verify reality.

## Install

Add the marketplace:

```
/plugin marketplace add amirshayegh/probe-loop
```

Install the plugin:

```
/plugin install probe-loop@probe-loop
```

Then reload:

```
/reload-plugins
```

## What it does

The probe loop is a five-stage verification pass that catches bugs surviving green test suites:

1. **Probe** the real production path
2. **Verify** the actual output, not the status code
3. **Discover** where report and reality diverge
4. **Fix** the root cause (rarely the layer that surfaced the symptom)
5. **Lock** the probe as a regression gate

It catches six categories of bug:

- **Silent no-ops** — the operation completes, output equals input, status says success
- **Environment mismatches** — correct against spec, broken against runtime
- **Swallowed errors** — failure path drops the diagnostic or returns truncated output
- **Hardcoded parameters** — works for one case, silently wrong for the rest
- **Cross-layer trust violations** — each layer assumes the other handled it
- **Destructive edge cases** — safe in the common case, destroys data in the corner

## Trigger phrases

The skill activates on prompts like:

- "Does this actually work?"
- "Verify this end-to-end."
- "Test against the real API."
- "Find bugs that survived testing."
- "Harden this."
- "The tests pass but I'm not sure if it actually works."

## When not to use

- New code being developed for the first time — use TDD
- Pure refactoring with no behavior change — use characterization tests
- Style, linting, or formatting passes

## Background

The probe loop is a verification practice that became affordable when agents could hold the codebase, the failure trace, and the regression-test draft inside a single context. The full rationale is at [shayegh.ca/blog](https://www.shayegh.ca/blog).

## License

MIT
