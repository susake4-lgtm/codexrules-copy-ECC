---
name: code-review-standard
description: Use after meaningful code, config, or script changes when a findings-first review against plan, correctness, regressions, and tests is needed.
---

# Code Review Standard

Use this skill after meaningful implementation changes.

## Announce

Start by stating that you are using `code-review-standard` for a findings-first review.

## Workflow

1. Identify the intended behavior, plan, or requirement the change is supposed to satisfy.
2. Check for plan or requirement mismatch first.
3. Check correctness and regression risk.
4. Check validation and test coverage gaps.
5. Check whether complexity increased without clear need.
6. Report concrete findings, or explicitly state that no findings were found.

## Output

For each finding, include:

1. severity
2. location
3. concrete risk
4. required fix or follow-up

If no findings exist, still report:

1. testing gaps
2. residual risk

