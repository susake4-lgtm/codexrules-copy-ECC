---
name: skill-create
description: Use when the user wants to create a reusable skill by analyzing local git history for repeated workflows, conventions, architecture patterns, and testing practices.
---

# Skill Create

Use this skill when the goal is to generate a new skill from evidence in a local Git repository rather than inventing one from scratch.

## Announce

Start by stating that you are using `skill-create` to mine local Git history for reusable patterns.

## Preconditions

1. Confirm the target directory is a Git repository.
2. Decide the analysis window, for example the last 100 to 200 commits.
3. Decide whether the result should become:
   - a project-specific skill or rule
   - a machine-wide reusable skill candidate

If the directory is not a Git repository, stop and explain that the workflow requires Git history.

## Workflow

1. Gather Git evidence. Typical commands:
   - `git log --oneline -n 200 --name-only --pretty=format:"%H|%s|%ad" --date=short`
   - `git log --oneline -n 200 | cut -d" " -f2- | head -50`
   - `git log --oneline -n 200 --name-only | grep -v "^$" | grep -v "^[a-f0-9]" | sort | uniq -c | sort -rn | head -20`
2. Identify repeated patterns such as:
   - commit conventions
   - file co-changes
   - workflow sequences
   - architecture or folder structure patterns
   - testing patterns
3. Separate stable patterns from one-off history noise.
4. Decide the target scope:
   - keep project-specific patterns in project-level rules or repo-local skills
   - only promote cross-project stable patterns to machine-wide skills
5. Draft a focused `SKILL.md` with:
   - clear trigger description
   - concise workflow
   - concrete output format
   - only the patterns supported by evidence
6. Report the evidence and the proposed skill path.

## Output

Always report:

1. repository analyzed
2. commit window used
3. strongest patterns found
4. proposed skill name
5. recommended target scope
6. generated or proposed skill path

## Notes

1. Prefer one focused skill over one large mixed skill.
2. If multiple unrelated patterns appear, split them into separate skill candidates.
3. Do not promote project quirks into machine-wide defaults without clear cross-project value.

