# LLM Coding Guidelines

Balanced coding guidelines for LLM-assisted software development.

These rules prioritize **correctness**, **clarity**, and **verifiable outcomes**, while preventing common failure modes such as overengineering, speculative features, and unnecessary refactors.

English | [简体中文](./README-ZH.md)

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

## Usage

- Place `instruction.md` in the project root or a designated documentation directory
- Reference this file in LLM prompts or development guidelines
- Use it as a standard for code review and validation

---

## Notes

This guide is not intended to restrict creativity, but to:

- Reduce unnecessary LLM overreach
- Minimize irrelevant refactoring
- Improve predictability and controllability of changes

---

## License

Apache License 2.0
