---
name: security-review-standard
description: Use when changes touch auth, permissions, secrets, external input, shell execution, file operations, network access, dependencies, or exposed surfaces.
---

# Security Review Standard

Use this skill for risk-triggered security review.

## Announce

Start by stating that you are using `security-review-standard` to evaluate whether the change introduces security-relevant risk.

## Workflow

1. Decide whether the change triggers security review.
2. If triggered, inspect:
   - input validation
   - secret handling
   - unsafe defaults
   - privilege boundaries
   - dangerous commands
   - untrusted sources
3. Decide whether any finding blocks completion.
4. Report remaining risk even if no blocking issue exists.

## Output

Always report:

1. whether security review was triggered
2. findings
3. impact
4. whether the issue blocks completion
5. residual risk

