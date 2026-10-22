---
name: maintain-formal-verification-skill
description: "Update an existing formal verification skill after covered code changes. Reconcile its model, harness, and properties with current code, then separate verification drift from code defects. Use for $maintain-formal-verification-skill or a stale formal model."
---

# Maintain a formal verification skill

Follow [the Codex runtime contract](../poteto-mode/references/codex-agent-runtime.md). Edit verification artifacts and their skill only. Do not fix product code without a separate request, or weaken a property to hide a defect.

1. Find project skills that run model checkers, provers, or code-level verifiers. Read the selected skill and collect each property, covered code, bounds, assumptions, command, and sync commit. If none exists, stop and point to [create-formal-verification-skill](../create-formal-verification-skill/SKILL.md). If no sync commit exists, use the last verification commit and state this assumption.
2. Run each check before edits. An old pass proves only the old description, not that the description still matches current code.
3. Read the covered-code diff and commit messages from the sync commit. Include uncommitted changes, renamed or moved functions, and new writers to guarded state. Classify each change as no effect, verification drift, an intended change to the promise, or a possible code defect.
4. Update the model or harness from the code, before looking for a passing result. Preserve atomicity, bounds, and assumptions unless the code requires a change. Change a property only when cited product evidence shows that its promise changed. Record old and new wording. Disclose any reduced bound.
5. Rerun. For a pass, use an isolated scratch mutation to show that the check still detects the guarded fault. Remove only that mutation and rerun. For a failure, replay the counterexample against current code. An impossible step indicates a modeling error. A feasible sequence is a code finding. Identify its introducing commit when evidence permits; otherwise state that it is unknown.
6. Update coverage, commands, bounds, assumptions, and sync commit. Do not advance the sync commit for a blocked check. If uncommitted product changes were included, record their patch identity as well. Follow the revised skill once as another agent would.

Report each check as `in sync`, `updated`, `bug`, or `blocked`. A check can be both updated and bug. Give the commits examined, verification changes and reasons, rerun result, mutation result, exclusions, and remaining coverage gaps. Explain counterexamples and harm in plain words. Distinguish verification drift from code defects, including an old pass that covered a stale model.

Keep verification changes separate from any later product fix.
