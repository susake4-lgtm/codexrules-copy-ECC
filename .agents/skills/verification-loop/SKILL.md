---
name: verification-loop
description: Use when code, config, scripts, or rules changed and a structured verification pass is needed before closure.
---

# Verification Loop

Use this skill after implementation and before final closure.

## Announce

Start by stating that you are using `verification-loop` to run the strongest meaningful verification path available.

## Workflow

1. Identify which verification capabilities exist in the current project.
2. Prefer this order when available:
   - build
   - typecheck
   - lint
   - test
   - security
   - debug or log residue checks
3. Run the strongest meaningful subset the project supports.
4. Record:
   - what was run
   - what passed
   - what failed
   - what is unavailable
   - what risk remains

## Output

Always report:

1. verification summary
2. missing checks
3. blocking failures
4. residual risk

