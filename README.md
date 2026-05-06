# LLM Coding Guidelines (Balanced Version)

Balanced coding guidelines for LLM-assisted software development.

These rules prioritize **correctness**, **clarity**, and **verifiable outcomes**, while preventing common failure modes such as overengineering, speculative features, and unnecessary refactors.

## Key Principles

- **Correctness > Clarity > Minimal Diff > Performance > Brevity**
- Do not optimize for fewer lines of code
- Prefer readable, testable implementations over clever shortcuts
- Make surgical changes by default, but fix root causes when necessary
- Avoid speculative abstractions and unrequested flexibility
- Require verification via tests or reproducible steps

## Intended Use

Use these guidelines as:

- A system prompt / coding policy for LLM tools
- A contributor rulebook for AI-assisted PRs
- A quality filter to reduce risky or overly broad diffs

## Install

See: `instruction.md`
