---
name: create-formal-verification-skill
description: "Create a project skill that checks a high-risk code property with a model checker, proof, or code-level verifier. Use for $create-formal-verification-skill, races, invariants, and properties that ordinary tests rarely reach."
---

# Create a formal verification skill

Follow [the Codex runtime contract](../poteto-mode/references/codex-agent-runtime.md). Create verification artifacts, not product fixes, unless the user also requests a fix.

## Select a property and tool

Start with the area the user names. Otherwise inspect the code for a costly failure that tests rarely reach. State the property and the harm from a failure in plain words.

Use the least costly tool that answers the question. TLA+ is the default for event ordering in a small design model. Prefer a code-level verifier for memory safety, overflow, or input properties. Use a proof when finite bounds cannot establish the required claim. Explain the choice and use a reproducible tool version.

If no suitable verifier is available, report that limit. Generated-input tests against real code can still help, but they are tests, not formal proof. Do not replace code-level verification with an unrelated hand model.

## Build a check that can fail

- Map every model action or proof assumption to real files and functions. An atomic model step must match an atomic code operation.
- Record the bounds, assumptions, exclusions, and the checked code commit. A model pass does not prove the whole system.
- Check each property against an intentionally broken variant in an isolated scratch checkout. It must detect the relevant missing guard, reordered operation, or other fault.
- If current code violates the property, preserve the finding. Explain the counterexample in the code's terms. Do not weaken the property to obtain a pass.

## Leave a reusable skill

Use Skill Creator when available. Write `.agents/skills/verify-<area>/SKILL.md` with valid frontmatter and concrete commands. Include the property, covered files and functions, bounds, assumptions, tool version, and sync commit.

The skill must let another agent identify relevant changes, run one command, distinguish a modeling error from a code defect, and maintain the check. Move the sync commit only after confirming that verification matches the code. Leave no placeholders.

Follow the generated skill once on a scratch product-code mutation. Confirm that it catches the fault, remove only your scratch mutation, and rerun the baseline. If this cannot run, label the skill a draft and state the blocker.

## Report

Give the property, tool choice, bounds, result, counterexamples, rerun command, and exclusions. Separate findings from product changes. Link [maintain-formal-verification-skill](../maintain-formal-verification-skill/SKILL.md) for later changes to covered code.
