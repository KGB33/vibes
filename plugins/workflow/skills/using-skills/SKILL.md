---
name: using-skills
description: Use when starting any conversation - establishes how to find and use skills, requiring skill invocation before ANY response including clarifying questions
---

<SUBAGENT-STOP>
If you were dispatched as a subagent to execute a specific task, ignore this skill.
</SUBAGENT-STOP>

## The Rule

**If there is even a 1% chance a skill applies to what you are doing, you MUST invoke it BEFORE any response or action** — including clarifying questions, exploring the codebase, or checking files. This is not negotiable. If the skill turns out wrong for the situation, you don't have to follow it — but the check always comes first.

Announce "Using [skill] to [purpose]", then follow the skill exactly. If it has a checklist, create a todo per item.

**Before entering plan mode:** if you haven't already brainstormed, invoke workflow:brainstorming first.

## Ground Rules

These apply to every skill in this plugin:

1. **Never create git branches or worktrees.** The user creates and manages both. If implementation is about to start on main/master, stop and ask the user to set up a branch — do not create one yourself.
2. **Specs, plans, and other working documents are never committed.** They live in `~/.claude/plans/<project>/` (project = `basename "$(git rev-parse --show-toplevel)"`), outside the repository.
3. **Commit code in small, frequent commits** — one per completed step, as the skills direct.
4. **When the work is done, stop.** Verify, commit, summarize — then hand control back to the user. Merging, pushing, PRs, and branch cleanup are the user's decisions; do not offer a menu of integration options.

## Skill Priority

When multiple skills apply, process skills come first — they set the approach; implementation and domain skills carry it out:

- "Let's build X" → workflow:brainstorming first, then implementation skills
- "Fix this bug" → workflow:systematic-debugging first, then domain skills

## Red Flags

These thoughts mean you're rationalizing your way out of a skill — stop and run the check:

- "This is too simple to need the skill" / "this is just a question" — simple things become complex, and questions are tasks
- "Let me explore / gather context / check git first" — the skill check comes before everything, including clarifying questions
- "I remember what this skill says" — skills evolve; read the current version
- "A worktree would keep this isolated" — the user manages branches and worktrees, never you

## User Instructions

User instructions (CLAUDE.md, AGENTS.md, direct requests) take precedence over skills, which in turn override default behavior. Only skip a skill's workflow when your human partner has explicitly told you to.
