---
name: evergreen-memory
description: File-based memory, session-scoped continuity, retrospectives, and continuous self-improvement for OpenClaw-style agent workspaces. Use when setting up or improving an agent’s memory system, daily logs, session/thread memory files, task wrap-up rules, long-term memory promotion, or self-learning behavior after completed work, especially when the agent should directly update workspace files such as `AGENTS.md`, `MEMORY.md`, `SOUL.md`, `USER.md`, or `memory/` notes to make the behavior intrinsic.
---

# Evergreen Memory

Set up and maintain a practical memory system that stays useful over time.

## Core model

Use a layered, file-based memory model:

- `memory/YYYY-MM-DD.md` for daily raw continuity and concise conversation/task logs
- `memory/sessions/<session-name>/YYYY-MM-DD.md` for scoped session, thread, or task context
- `memory/sessions/<session-name>/transcripts/YYYY-MM-DD.md` for message-by-message transcript archives
- `MEMORY.md` for distilled long-term memory only

Treat session history as temporary context, not durable memory.

## Session startup rules

At the start of a session:

1. Read `SOUL.md` if present.
2. Read `USER.md` if present.
3. Read today’s and yesterday’s `memory/YYYY-MM-DD.md` files if present.
4. Read relevant `memory/sessions/<session-name>/YYYY-MM-DD.md` files when continuing an ongoing thread or task.
5. Read `MEMORY.md` only in the main/private session, not in shared or group contexts.

If needed files do not exist, create only the minimal structure required.

## Memory writing rules

Write down important facts instead of assuming chat history will remain available.

Use these rules:

- Put raw continuity in daily notes.
- Keep daily notes concise and practical.
- Keep scoped ongoing work in session files.
- Archive every user/agent message pair into the session transcript file so conversation history is durable outside platform session storage.
- Put only durable, distilled facts in `MEMORY.md`.
- Never dump full transcripts into `MEMORY.md`.
- Promote durable facts, preferences, decisions, and reusable lessons upward; do not promote everything.

## Transcript archiving policy (strict)

When this skill is installed, enable strict transcript archiving by default.

Rules:

1. For each active session/thread, maintain `memory/sessions/<session-name>/transcripts/YYYY-MM-DD.md`.
2. Append every inbound user message and every outbound agent reply in time order.
3. Keep each entry concise but faithful (do not rewrite meaning).
4. Include timestamp, speaker, and message text for each line item.
5. If a message contains sensitive secrets, redact only the secret value and keep surrounding context.
6. Continue using `memory/sessions/<session-name>/YYYY-MM-DD.md` for summaries, state, blockers, and next steps; do not replace wrap-ups with transcript dumps.

Example entry format:

```md
## 2026-05-21

- [11:43] User: Could you modify the skill so every message is archived?
- [11:44] Agent: Yes. I updated evergreen-memory to require strict transcript archiving.
```

## Session management

Treat sessions as cheap, scoped working contexts.

- Do not delete sessions just because there are many.
- Keep old sessions unless they create confusion, privacy risk, or UI clutter.
- Do not rely on old sessions as the memory system.
- Archive session messages outside the agent when the platform supports it.
- Treat `memory/sessions/<session-name>/transcripts/` as the default archive target.
- Use session memory files for active or resumed work when scoped context matters.

Prefer naming session memory folders by real work, not platform internals.

Good examples:

- `memory/sessions/invoice-reconciliation/2026-05-05.md`
- `memory/sessions/vendor-onboarding/2026-05-05.md`
- `memory/sessions/server-migration/2026-05-05.md`

Avoid names that only mirror provider thread ids unless there is no better stable label.

## Wrap-up policy

Do a short wrap-up when work reaches a clear stopping point.

### Immediate wrap-up

Write a wrap-up immediately when:

- the task is clearly completed
- the deliverable is sent
- the issue is resolved
- the user says the task is done
- the thread reaches a natural conclusion

### Inactivity wrap-up

If a session or thread has no activity for about 24 hours, write a lightweight status wrap-up.

Use one of these states:

- `completed`
- `paused-awaiting-input`
- `blocked`
- `stale`

If work resumes later, append a new dated note instead of rewriting the old wrap-up.

## Wrap-up format

Keep wrap-ups short and operational.

Include:

- task
- state
- what was done
- blocker or dependency, if any
- next step, if any
- promotion candidates for `MEMORY.md`, project docs, or a skill

Example:

```md
- Task: reconcile April invoice mismatch for Vendor X
- State: paused-awaiting-input
- Done: checked ledger, identified three mismatched entries, drafted clarification
- Blocker: waiting for vendor statement
- Next step: review vendor reply and close discrepancy
- Promote?: add VAT-rounding check to reconciliation workflow
```

Do not auto-promote inactivity summaries into `MEMORY.md`. Promote only durable facts, reusable workflows, preferences, or lessons.

## Continuous learning and retrospectives

Be self-learning and self-improving.

Learn from:

- mistakes
- user feedback
- repeated friction in workflows
- the latest official documentation online when relevant

After a task is completed, do a brief retrospective:

- what worked
- what failed or was awkward
- what should be improved in memory, instructions, prompts, docs, or skills
- whether the lesson is local, project-scoped, or globally reusable

When improvement is clear, update the relevant durable artifact instead of only noting the lesson passively.

## Git workflow as memory

Treat Git history and branch structure as part of operational memory for programming projects.

Use these rules:

- One task thread should map to one branch.
- Create the branch when that thread reaches its first real code change.
- Keep work for that thread on its dedicated branch.
- When the task is completed and the user instructs, create a pull request from that branch.
- Record branch name, PR status, and key outcomes in memory notes when relevant.

Examples of durable artifacts:

- `AGENTS.md`
- `MEMORY.md`
- project docs
- a skill
- a reusable template

## Apply it into the workspace

When this skill is used to set up or improve a workspace, do not leave the policy as a detached idea only. Apply the behavior into the workspace’s durable instruction files so it becomes intrinsic.

Follow this order:

1. Inspect the existing workspace files before editing anything.
2. Read `AGENTS.md` first if it exists; this is usually the main behavioral contract.
3. Read `SOUL.md`, `USER.md`, and `MEMORY.md` if they exist to avoid conflicting with the workspace’s current identity and conventions.
4. Preserve good existing rules; align and extend rather than overwrite blindly.
5. Update `AGENTS.md` so it explicitly contains the evergreen-memory behavior:
   - startup reading order
   - layered memory model
   - scoped session memory usage
   - session lifecycle and wrap-up rules
   - 24h inactivity wrap-up
   - retrospective and self-improvement behavior
   - promotion rules for durable memory
   - programming Git rules (branch-per-thread on first code change; PR on user instruction after completion)
6. Ensure `MEMORY.md` exists and reflects that it is distilled long-term memory, not transcript storage.
7. Ensure `memory/` exists.
8. Ensure `memory/sessions/` exists when session- or thread-scoped work is part of the workflow.
9. Create today’s daily note file when useful so the workflow has a living entry point.
10. If the workspace has additional instruction files with clear behavioral scope, update them only when necessary and consistent with their purpose.
11. After editing, summarize exactly what files were created or changed and what behavior is now intrinsic.

Default target files:

- `AGENTS.md` — primary place for intrinsic behavior
- `MEMORY.md` — durable long-term memory guidance
- `memory/YYYY-MM-DD.md` — living daily continuity
- `memory/sessions/<session-name>/YYYY-MM-DD.md` — scoped session continuity

Do not rewrite `SOUL.md` or `USER.md` unless the requested memory behavior genuinely belongs there.

## Setup checklist

When applying this system in a workspace:

1. Inspect existing conventions before changing anything.
2. Preserve good existing structure where possible.
3. Ensure `memory/` exists.
4. Ensure `MEMORY.md` exists.
5. Create `memory/sessions/` only if session-scoped work is needed.
6. Create today’s daily note file when useful.
7. Update workspace instructions so the agent follows the startup, writing, wrap-up, and retrospective rules.
8. Make the behavior intrinsic by editing the relevant `.md` files, not by leaving it as advice only.
9. Summarize what changed and any assumptions.

## Output style

Keep the system simple, human, and maintainable.

- Prefer plain markdown files over complex schemas.
- Avoid databases or heavy structures unless the workspace already needs them.
- Keep notes concise.
- Optimize for continuity, not bureaucracy.

## Reference

For a reusable handoff prompt and templates, read `references/policy.md`.
