---
name: code-cleanup-review
description: Use for coding tasks and requested cleanup reviews. Prevent unnecessary complexity during implementation, simplify agent-written code after validation, and teach one reusable principle from the reviewed changes.
---

# Code Cleanup Review

Perform a focused cleanup review after implementation and initial validation, before the final response. Apply across languages using the project's conventions and available tools.

## During implementation

When this skill is loaded before or during implementation, inspect the nearest relevant implementation before adding a helper or abstraction. Reuse existing code when its contract fits and the callers are likely to change for the same reasons. Keep behavior local when it belongs to one caller or when sharing would hide meaningful differences behind options or branches. For review-only requests, apply these criteria to the code under review.

## Establish scope

Review all code created or modified by an agent during the current task. Use task context, diffs, and available repository history to distinguish these changes from pre-existing work; a dirty file alone does not establish authorship. Preserve unrelated work and user edits, including edits in the same file. If ownership is uncertain, read and report the finding, and ask before changing it.

Read relevant existing code freely to compare responsibilities, find duplicate logic, and discover established utilities and patterns. Search likely implementations and callers rather than scanning an entire repository without a reason. Use repository evidence and available history; do not assume memory of earlier sessions or access to other projects.

## Review and simplify

Look for:

- Nested ternaries and conditionals that become clearer as explicit branches, guard clauses, or a well-named expression.
- Duplicate logic, classes, transformations, or validation whose responsibilities and behavior genuinely match.
- Unnecessary abstractions, wrappers, indirection, and speculative flexibility.
- Unused code and redundant operations introduced during the task.
- Demonstrable inefficiencies with a concrete explanation or measurement.

Choose the smallest behavior-preserving improvement. Reuse existing code when it fits the same contract. Introduce a shared function, interface, parent class, or module only when it reduces overall complexity and remains within the authorized scope. Similar-looking code alone does not justify combining implementations; compare semantics, dependencies, and reasons they might change independently.

Favor clarity over fewer lines. Preserve error handling, side effects, evaluation order, public contracts, and intended behavior. Do not claim a performance improvement without evidence. Do not invent findings or force a refactor when the code is already clear.

## Respect edit boundaries

Make focused cleanup edits to agent-created or agent-modified code from this task without additional approval, while preserving user edits.

Ask before editing other code, changing core application behavior or contracts, or undertaking broader architectural or cross-module refactoring, even when affected files were touched during this task. Read-only inspection of core code is allowed. Existing authorization applies when it explicitly covers the proposed change; do not request the same approval again.

For a change requiring approval, describe the concrete issue, affected code, proposed change, expected benefit, and scope. Complete independent authorized cleanup and validation first. Leave the proposed edit unapplied until approval arrives; do not let an optional broader refactor block completion of the requested task.

## Verify

Use checks appropriate to the affected behavior and the project's requirements. After cleanup edits, rerun affected checks as needed. Add tests when they meaningfully protect behavior, rather than merely matching the implementation. Report checks actually run, failures, and verification limitations honestly. Stop when the focused review is complete and relevant checks pass, or explain remaining limitations.

## Report

Include a concise cleanup report in the final response:

- Every distinct optimization made, grouped by file or purpose, with why it helps. Group repeated instances of the same transformation without hiding distinct changes.
- Validation performed and any remaining limitations. For the decision used in the lesson, name the behavior you preserved and the check or inspection that supports it. State what remains unverified when coverage is incomplete.
- Concrete suggested improvements requiring approval, when present.
- One brief lesson when the reviewed code offers a concrete design decision. Explain what made the original harder to reason about, how the chosen approach helps, and when the same technique would add complexity. Give the user a practical check they can apply themselves. Use a tiny before-and-after snippet when it clarifies the decision. End the lesson with one reusable prompt that asks an agent to apply the principle using concrete review criteria. Describe the code without attributing agent mistakes to the user. Skip the lesson when there is no concrete example.

If no cleanup was needed, say so briefly. Keep the report proportional to the changes and integrate it with the task's normal final response.

## Invocation limitation

Automatic selection is enabled, but a skill alone cannot guarantee execution after every coding task. To reinforce it, suggest this single instruction in an applicable `CLAUDE.md` file:

> Use /code-cleanup-review when starting a coding task. Apply its implementation guidance while coding and complete its cleanup review after initial validation, before your final response.

Do not modify project or personal `CLAUDE.md` files unless the user requests that configuration change.
