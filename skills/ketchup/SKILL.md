---
name: ketchup
description: "Summarize this chat since the user's previous message and list every pending user decision with enough context to act. Use for $ketchup. Keep the request read-only."
---

# Ketchup

Use [bro](../bro/SKILL.md)'s plain voice. Follow [the Codex runtime contract](../poteto-mode/references/codex-agent-runtime.md). Rebuild what changed since the last human message before this invocation. Agent results and notifications do not reset that point.

## Gather

Keep this turn read-only. Inspect current PR, CI, and agent state only for work this chat touched. Use existing evidence; do not change code, start an app or job, or post a message. Correct any stale number you report.

Collect every unresolved decision or action only the user can take, including older ones. Do not label work you can still do yourself as a user action. For each item, gather its link, user impact, evidence, risk, and recommendation. Mark required facts unknown when evidence is missing. Do not invent links or decisions.

## Report

Open with what waits on the user, or say that nothing does. If nothing changed and nothing waits, stop.

Keep the change summary under 100 words when possible. Say what each requested task achieved and whether it is complete, running, failed, or unverified. Do not call work complete while it needs a user decision. Name work you can still do yourself separately.

List every pending item. Never replace items with a count or omit them to meet a word limit. The reply must be sufficient to decide without opening its links. Group items that share a decision, state the recommendation once, and give each item its link, impact, evidence, and risk. Order grouped items by risk. For a choice, give every considered option and its gain and cost. State a waiting cost only when it exceeds ordinary delay.

Embed existing screenshots or videos when they explain a visible change. If none exists, say what changed and that no screenshot is available. Use a compact diagram or chart only when relationships or numbers are easier to understand that way. Do not turn a status list into boxes or repeat the same fact in prose and a visual. Never invent a number or simulate an uncaptured screen.
