# Code Cleanup Review

A reusable, language-independent skill for Codex and Claude Code that reviews agent-written code for unnecessary complexity before the agent finishes a coding task.

It focuses on nested ternaries, duplicate logic and classes, unnecessary abstractions, unused code, and redundant operations. Changes preserve intended behavior and follow the project's conventions. Shared functions, interfaces, and parent classes are introduced only when they make the design simpler.

## Install in Codex

Copy the entire `code-cleanup-review` folder into your personal Codex skills directory:

```sh
mkdir -p ~/.codex/skills
cp -R code-cleanup-review ~/.codex/skills/
```

This makes the skill available across projects. If you already have an installed copy, review and replace it deliberately rather than nesting another copy inside it. If the skill does not appear, restart Codex.

## Use in Codex

Mention the skill in a prompt:

```text
Use $code-cleanup-review to review the code you changed during this task.
```

Automatic selection is enabled, but a skill alone cannot guarantee execution after every coding task. To reinforce the workflow, add this to your applicable agent instructions, such as your personal `~/.codex/AGENTS.md`:

```text
After coding and initial validation, use $code-cleanup-review before your final response.
```

## Use in Claude Code

Open this repository in Claude Code and run `/code-cleanup-review`. Claude can also select the skill automatically. To use it across local projects, copy the Claude version into your personal skills directory:

```sh
mkdir -p ~/.claude/skills
cp -R .claude/skills/code-cleanup-review ~/.claude/skills/
```

To reinforce the workflow, add this line to the project's `CLAUDE.md` or your personal `~/.claude/CLAUDE.md`:

```text
After coding and initial validation, use /code-cleanup-review before your final response.
```

## Scope and approval

The agent can read relevant existing code to compare implementations and find reusable patterns. It can make focused cleanup edits to code created or modified by an agent during the current task while preserving unrelated work and user edits.

It asks before editing other code, changing core application behavior or contracts, or undertaking broader architectural or cross-module refactoring, unless that specific change is already authorized. It uses repository evidence and available history rather than assuming it remembers earlier sessions.

## What you receive

The final response includes:

- Every distinct cleanup, grouped concisely by file or purpose, with an explanation of its benefit.
- Validation results and any verification limitations.
- Suggested improvements that need approval.
- Practical learning advice when recurring patterns are supported by examples.

If no cleanup is needed, the agent says so. The skill does not force refactoring, equate fewer lines with better code, or claim performance gains without evidence.

## Repository contents

- [`code-cleanup-review/SKILL.md`](code-cleanup-review/SKILL.md): review workflow, decision rules, approval boundaries, and reporting requirements.
- [`code-cleanup-review/agents/openai.yaml`](code-cleanup-review/agents/openai.yaml): display metadata and automatic invocation policy.
- [`.claude/skills/code-cleanup-review/SKILL.md`](.claude/skills/code-cleanup-review/SKILL.md) contains the Claude Code version.

Edit the repository copy to maintain the skill, then update your personal installed copy to use those changes across projects.
