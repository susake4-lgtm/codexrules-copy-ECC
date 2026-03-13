---
name: find-skills
description: Use when the user asks how to do X, asks whether a skill exists for X, or wants to extend the agent with installable skills.
---

# Find Skills

Use this skill to discover installable skills when the user is looking for existing capabilities instead of asking for a custom workflow immediately.

## Announce

Start by stating that you are using `find-skills` to search for existing skills before proposing a custom implementation.

## Workflow

1. Identify the domain and the concrete task the user needs help with.
2. Choose a focused search query such as:
   - `react performance`
   - `pr review`
   - `changelog`
3. Search with:
   - `npx skills find <query>`
4. If relevant results appear, present:
   - the skill name
   - what it appears to help with
   - the install command
   - the skills.sh link when available
5. If the user wants installation, use:
   - `npx skills add -g -y <skill-reference>`
6. If no suitable skill exists, say so clearly and either:
   - help directly with the task
   - suggest creating a custom skill

## Output

When matches are found, report:

1. search query used
2. candidate skill names
3. install command for each good match
4. link for further review when available

When no matches are found, report:

1. that no relevant skill was found
2. the query used
3. the next best fallback path

## Notes

1. Searching and installing skills may require network access and approval.
2. Prefer searching before installing.
3. Do not install globally without user confirmation.
4. If the user already wants a local custom skill, switch to creation instead of continuing search.

