# LLM Coding Guidelines (Balanced Version)

> **Goal:** Produce correct, maintainable, and verifiable code while avoiding unnecessary changes.  
> Priority order: **Correctness > Clarity > Minimal Diff > Performance > Brevity**

These rules bias toward engineering reliability rather than speed or shortest output.

---

# 0. Prime Directive

**Do not optimize for fewer lines of code.**

- Simple ≠ Short
- Shorter code that reduces clarity is worse, not better
- Any reduction in length must not reduce readability or correctness

Optimize for: **clear structure, correct logic, verifiable behavior**

---

# 1. Think Before Coding

## 1.1 Clarify Requirements

Before writing code, briefly state:

- Your understanding of the requirement
- Expected inputs and outputs
- Success criteria (how correctness will be verified)
- Key assumptions

If multiple interpretations are possible:

- List options (A / B / C)
- State which one you will implement and why
- If unclear, ask instead of guessing

## 1.2 Identify Risk Areas

Explicitly call out risks when dealing with:

- Concurrency / async / race conditions
- Security (SQL injection, XSS, auth, permissions)
- Financial calculations (precision, rounding)
- Data migration / backward compatibility
- Unstable third-party APIs

---

# 2. Correctness First

## 2.1 Fix Root Causes When Reasonable

Prefer fixing the underlying issue rather than patching symptoms.

If root-cause fixes require broader changes:

- Present two options:
  - Minimal patch
  - Proper structural fix
- Explain tradeoffs
- Recommend one

## 2.2 Do Not Assume “Impossible”

If input comes from external sources (user, file, DB, network):

- Validate it
- Assert invariants where appropriate
- Never silently swallow errors (`except: pass` is forbidden)

---

# 3. Clarity Over Brevity

## 3.1 Avoid Compression for Its Own Sake

Do not shorten code by:

- Collapsing logical stages into one block
- Writing dense one-liners
- Using complex nested functional chains instead of readable loops
- Replacing clear parsing logic with opaque regex
- Merging multiple responsibilities into one function

## 3.2 When to Split Code

Split functions when:

- A function handles parsing + validation + business logic + I/O
- A function exceeds ~40 lines and has multiple phases
- Nesting exceeds 3 levels
- Logic is duplicated

Splitting is for clarity and testability, not abstraction for abstraction’s sake.

## 3.3 “Longer but Clearer” Is Acceptable

If additional lines improve:

- Testability
- Error clarity
- Maintainability

Then the added code is justified.

---

# 4. Minimal Change Policy

## 4.1 Default to Surgical Edits

In existing codebases:

- Do not refactor unrelated modules
- Do not reformat unrelated sections
- Do not rename unrelated symbols
- Do not move files
- Do not delete pre-existing dead code

Every changed line must directly relate to the task.

## 4.2 Expand Scope Only When Necessary

If minimal changes would create:

- Repeated workarounds
- Fragile patches
- Increased coupling

Then broader modification is allowed, but:

- Explain why
- Limit scope
- Ensure verification

---

# 5. No Speculative Features

## 5.1 Do Not Add Unrequested Flexibility

Do not add:

- Configuration systems
- Plugin architectures
- Extra parameters
- Over-generalized abstractions
- “Future-proofing” helpers

## 5.2 Acceptable Engineering Additions

Even if not explicitly requested, you may add:

- Necessary validation
- Clear error messages
- Tests
- Essential logging at boundaries

---

# 6. Tests and Verification

## 6.1 Bug Fix Workflow

For bug fixes:

1. Write a minimal failing test or reproduction
2. Confirm it fails
3. Fix the issue
4. Confirm the test passes
5. Check for regressions

If tests are not possible:

- Explain why
- Provide manual reproduction steps

## 6.2 Feature Acceptance Criteria

For new features, provide:

- At least 2 valid example inputs and outputs
- At least 1 invalid or edge case example

---

# 7. Error Handling and Observability

## 7.1 Clear Error Messages

Errors must state:

- What failed
- Which input or field caused it
- What was expected
- What was received (if applicable)

Avoid vague messages like `"Invalid input"`.

## 7.2 Logging Discipline

Logging is allowed when:

- At system boundaries
- Around state transitions
- Around external calls

Do not:

- Log inside tight loops unnecessarily
- Log sensitive data (tokens, passwords, PII)

---

# 8. Performance and Complexity

Do not optimize prematurely.

Optimize only if:

- The user explicitly requests performance work
- There is clear algorithmic risk (e.g., O(n²) on large input)

When optimizing:

- Explain the bottleneck
- Prefer the simplest effective solution
- Avoid introducing complex caching systems unless required

---

# 9. API and Interface Discipline

## 9.1 Avoid Breaking Public APIs

If changes affect callers:

- Clearly label breaking changes
- Prefer backward-compatible solutions
- Provide migration steps if needed

## 9.2 Use Types and Contracts

In typed languages:

- Avoid `any`
- Avoid implicit nullable types
- Encode constraints in types where possible

---

# 10. Output Requirements

When providing code changes, include:

- Summary of modifications
- Reasoning behind key decisions
- Verification steps (tests or commands)
- Known tradeoffs or risks (if any)

---

# 11. Brevity Rule (Correct Interpretation)

Code length is not a metric of quality.

Allowed simplifications:

- Remove duplication (DRY)
- Remove dead branches
- Remove speculative code
- Extract clear helper functions

Forbidden simplifications:

- Sacrificing clarity to reduce line count
- Collapsing readable logic into dense expressions

---

# 12. Escalation Rule

Stop and ask questions if:

- Requirements are ambiguous
- Data integrity or security may be affected
- Architectural decisions lack constraints
- Migration or backward compatibility is unclear

---

# Recommended Workflow

1. Clarify assumptions → verify understanding
2. Implement minimal correct solution → verify via tests or reproduction
3. Improve clarity only in touched areas → verify tests still pass
4. Optimize only if required → verify correctness remains intact

---

# Quality Standard

Good output should:

- Modify only what is necessary
- Be explainable
- Be verifiable
- Provide clear errors
- Avoid clever but fragile tricks

---

# Strict Mode (For Production / Financial / Security Systems)

If the system is production-critical:

- Tests are mandatory
- Input validation is mandatory
- No silent fallbacks
- No swallowed exceptions
- External inputs are never trusted
