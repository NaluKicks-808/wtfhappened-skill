---
name: wtfhappened
description: Structured postmortem when the user catches a mistake or something breaks: reconstruct how it happened, name the systemic gap, install a fix in the same session, and log it. Trigger: "/wtfhappened", "why did I catch that?", "how did that happen?", "what went wrong there?"
---

# wtfhappened: the postmortem skill

Born from a near-miss where a piece of work updated one record but not another that depended on it, and the user, not any automated check, caught the gap by asking whether the second record had been updated too. The retrospective that followed is this skill.

## When to run

Any time the user catches an error, an omission, or a broken promise of one of their systems, or asks any flavor of "why did that happen?" Do NOT run it for trivial slips being fixed inline; it's for failures that reveal something about the *system*, not the moment.

## The protocol: four questions, answered honestly, in order

Work from evidence (session history, logs, file states, the actual tool output), not vibes. Blameless toward the user, unsparing toward the process.

1. **Why was it caught the way it was?** Who or what noticed: the user, an automated gate, luck? If a human was the only audit, say so plainly: that is itself a finding. Identify the check that *should* have fired and whether it exists, exists-but-skipped, or doesn't exist.

2. **How was the mistake actually made?** Reconstruct the concrete sequence: what was produced, where it went, which step got skipped or shortcut, and what the session was optimizing for at the time (speed, momentum, a big docket). Name the anti-pattern if one fits (e.g., "log-line as tombstone": recording THAT something was learned instead of recording it where it belongs).

3. **What systemic gap allowed it?** Distinguish the two classic cases: **an unused system** (the rule/gate existed and was skipped; ask why skipping was possible at all) vs **a missing system** (no rule covered this boundary). Boundaries are where most gaps live: between one project and another, between a working draft and the canonical record, between "noted" and "done."

4. **What fixes prevent recurrence?** Cap at the BEST fix set, not a fixed number: one fix if one closes the gap, several if the gap genuinely needs several. Prefer, in order: (a) **structural**, make the failure impossible or blocking (a hook, a gate, a schema), over (b) **procedural**, a written rule the session must follow, over (c) **memorial**, a memory/note (weakest; use only to reinforce a or b). Every fix listed must be installed and verified in THIS session, a fix you won't install today doesn't belong in the list, and padding with weak fixes is how none of them ship. If a genuinely needed fix can't be installed today, put it on whatever ongoing task list you keep, with a clear trigger for when it fires, not in the fix list.

## The non-negotiable: install the fix NOW

The fix is implemented in the same session: a hook written, a rule added to the relevant instructions file, a script patched. A postmortem without an installed fix is a complaint, not a postmortem. Then verify the fix fires (run the hook, trip the gate deliberately if cheap).

## Log it

Append the incident to a postmortems file in your notes (create one from a simple format if you don't have one yet: date, what happened, the four answers, fixes installed). Commit and push if that's how you save your notes. If the fix changed an automation or standing system, update whatever file documents your running systems, so the two never drift apart.

## Output to the user

Answer the four questions in plain language, in order, keeping each to a short paragraph. Lead with the most uncomfortable true sentence (e.g., "the gate existed and I skipped it every time"). End with what's now installed and how they'd know it's working.
