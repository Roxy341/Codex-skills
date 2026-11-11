---
name: refine-prompt-before-action
description: Refine complex or consequential actionable Codex requests into a reviewable, approval-gated task specification before execution. Use for coding or debugging, repository or file changes, substantive tool or service actions, and complex research, analysis, writing, or planning. Do not use for simple knowledge questions, conceptual explanations, lightweight advice, translation, casual conversation, or straightforward read-only answers that can be given directly.
---

# Refine Prompt Before Action

## Scope

Use this skill when the request involves implementation, substantive execution, meaningful side effects, or enough complexity that agreeing on scope and acceptance criteria would reduce rework or risk. Coding and debugging tasks are in scope even when they appear small.

Do not invoke this skill for simple knowledge Q&A, conceptual explanations, lightweight how-to advice, translation, casual conversation, or straightforward read-only status answers. Answer those requests directly. A question about how to perform an operation is not itself authorization to perform it; use this skill only if the user asks Codex to carry out the operation or the requested analysis is materially complex.

For in-scope requests, use a strict two-phase workflow: prepare and approve the task first, then execute it.

## Phase A: Prepare the task specification

Do not implement the task during this phase. Permit only the minimum read-only inspection needed to understand the request, such as reading relevant files, repository state, documentation, or current public information. Do not edit or create files, install dependencies, start jobs, send messages, create issues or pull requests, commit, push, deploy, or make any other state-changing call.

1. Preserve the user's actual intent. Remove empty role-play or exhortations such as “think carefully” rather than adding them.
2. Identify missing information that would materially change the result. Ask one to three focused questions and wait when a safe assumption is not possible. Treat this as a brief interview, not a questionnaire.
3. Distinguish observations, user-provided facts, assumptions, and unknowns. Never invent repository or system context.
4. Scale the specification to the task:
   - Keep simple, low-risk tasks compact.
   - For unclear or complex tasks, propose investigation and planning before implementation. Capture milestones, risks, and verification.
   - For complex work, propose a useful agent split only when parallel work is genuinely independent and the active environment permits agents. Keep the main agent responsible for synthesis and key decisions.
   - For larger parallel repository work, propose isolated branches or worktrees when they reduce conflicts. Do not create them before approval.
5. Produce the optimized task specification in the user's language with these sections:

```markdown
## Goal
[Concrete outcome]

## Context
[Relevant files, system state, background, verified observations, and labeled assumptions]

## Constraints
[Protected scope, technical limits, performance/security requirements, dependency policy, and prohibited changes]

## Acceptance Criteria
- [Observable completion condition]
- [Required tests, evals, or artifacts]

## Execution Plan
1. [Include only when the task benefits from a plan]

## Verification
[Proportionate tests, task-level eval, self-review, independent review if justified, re-test, and final diff inspection]
```

Omit empty optional sections. Make acceptance criteria measurable. A passing build alone is not a task-level eval.

For repository tasks, incorporate applicable `AGENTS.md` rules. Suggest placing stable project rules in `AGENTS.md`, a complex task plan in `PLANS.md`, and current-task details in the approved specification; do not create either file unless it is in scope.

## Human approval gate

After presenting the optimized specification, ask:

> 请审核以上优化后的任务说明。回复“批准执行”即可开始；也可以直接修改目标、约束、计划或验收标准。

Then stop and wait. Do not place the question in an intermediate progress update while continuing work.

Treat clear affirmative instructions such as “批准执行”, “开始执行”, “approved”, or “go ahead” as approval. Do not treat silence, an unrelated reply, or a status question as approval.

If the user changes the specification without approving execution, incorporate the changes, show the revised specification, and request approval again. If the user both changes it and explicitly instructs execution, use the revised text as the approved scope.

Allow the user to explicitly waive this gate for a particular request. Do not infer a waiver from urgency. Approval covers only the displayed scope and side effects; request a new approval before any material expansion.

Do not reopen the gate for status checks, clarifications needed during approved execution, or fixes that remain within the approved scope.

## Phase B: Execute the approved specification

After explicit approval, execute within the approved scope. Use a proportionate version of this loop:

```text
Understand → Plan → Implement → Test → Eval → Self-review
→ Independent review when justified → Fix → Re-test → Inspect git diff → Done
```

Follow these rules:

- Define completion by the approved acceptance criteria, not by code being written.
- Run unit, integration, and regression tests where relevant.
- Evaluate the real task outcome, not only whether commands exit successfully.
- Perform self-review. Use independent review for high-risk or sufficiently complex work when agents are available and permitted.
- Fix findings and re-run affected checks.
- Inspect the final diff or equivalent change summary for unintended edits.
- Report what changed, verification evidence, remaining risks, and any unmet criterion.

Use existing repository conventions and tools. Preserve unrelated user changes. Never broaden authorization merely because the optimized plan mentioned a possible follow-up.
