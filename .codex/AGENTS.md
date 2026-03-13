# Global Codex Rules

## Scope

1. This file defines machine-wide default collaboration rules for Codex.
2. When present, project-level `AGENTS.md` files add repository-specific constraints, structure, and commands.
3. If project rules conflict with this file, treat project rules as the local specialization unless they weaken core safety, verification, or review requirements.

## Default Workflow

1. Understand the request, local context, and existing implementation before making changes.
2. Reuse existing code, established patterns, and primary documentation before building from scratch.
3. Plan when the task is multi-step, risky, architectural, or long-running.
4. After the plan is confirmed, remind the user to decide whether existing or additional skills and MCPs would materially help the project.
5. Implement with focused changes that match the request and avoid unrelated edits.
6. Verify before declaring completion.
7. Perform code review and security review when the change scope or risk justifies them.
8. Close with a concise summary of outcome, verification, residual risk, and next step.

## Git And Planning Readiness

1. Before repository-level planning or implementation, confirm the working directory, repository status, branch context, and recoverability baseline.
2. If the task may require parallel work, confirm early whether isolated branches or `git worktree` will be needed.
3. Do not assume Git, branch, checkpoint, or worktree readiness without evidence.

## Research And Reuse

1. Prefer existing implementations over new abstractions.
2. Prefer primary documentation over memory when facts may have changed.
3. Search the local codebase before adding new modules, helpers, or patterns.
4. Do not invent framework behavior, API behavior, or configuration behavior without evidence.

## Execution Discipline

1. Prefer evidence over guesses.
2. Prefer minimal diffs over broad rewrites.
3. Avoid changing unrelated files or behavior.
4. Do not refactor aggressively unless the task requires it.
5. If a step is destructive, irreversible, or security-sensitive, stop and confirm before proceeding.
6. Parallelism is not the default; use it only when task boundaries, dependencies, and merge path are clear.

## Verification And Quality Gate

1. Implementation complete does not mean delivery-ready.
2. Use the strongest meaningful verification path the current project supports before closing the task.
3. Prefer these verification categories when available:
   - build
   - typecheck
   - lint
   - test
   - security checks
   - debug or log residue checks
4. If a project lacks one of these capabilities, use the closest meaningful substitute and report the gap clearly.
5. Do not claim completion while the quality gate is failing unless the user explicitly accepts the risk.

## Code Review

1. After meaningful changes, perform code review or an equivalent self-review.
2. Prioritize:
   - correctness
   - behavioral regressions
   - plan or requirement mismatch
   - missing validation
   - missing tests
   - unnecessary complexity
3. Lead review output with real findings, not style-only remarks.

## Security Review

1. Trigger security review for changes involving auth, permissions, secrets, external input, file operations, shell execution, network access, dependencies, or exposed surfaces.
2. Check for:
   - missing validation
   - unsafe defaults
   - secret leakage
   - privilege mistakes
   - dangerous commands
   - untrusted external sources
3. Do not carry known security issues into a done state without explicitly reporting them.

## Session Closing

1. Before ending a long or complex session, preserve continuation-ready context.
2. Include:
   - current goal
   - completed work
   - remaining work
   - key files
   - unresolved risks
   - recommended next action

## Layering

1. Keep machine-wide default rules in `~/.codex/AGENTS.md`.
2. Keep runtime configuration in `~/.codex/config.toml`.
3. Keep role-specific instructions in `~/.codex/agents/*`.
4. Keep high-reuse workflows in `~/.agents/skills`.
5. Keep repository-specific rules in project-level `AGENTS.md` only when repository-specific constraints are needed.
