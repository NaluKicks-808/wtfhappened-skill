# wtfhappened

A Claude Code skill that runs a structured postmortem whenever you catch a mistake in your own systems. It walks through four questions in order, then installs a real fix in the same session instead of just writing the incident down.

## Start here

1. Download this repository (the green "Code" button, then "Download ZIP", or `git clone` if you use git).
2. Copy the `skills/wtfhappened` folder into `~/.claude/skills/` on your computer.
3. Restart Claude Code.
4. Type `/wtfhappened` after you notice something went wrong, for example `/wtfhappened the newsletter went out with last week's numbers`.

## Example

> **You:** /wtfhappened I just found out the report emailed to the client still had last month's totals in it
>
> **Claude:** Why was it caught the way it was? The client noticed, not any check on our end. How was the mistake made? The report template pulls from a file that gets updated manually, and this month nobody updated it before sending. What systemic gap allowed it? There's no step that checks the data's date before send. What fixes prevent recurrence? Adding an automated check that blocks sending if the data is older than a set number of days. [Claude then writes and tests that check before finishing.]

## Honest limit

The skill insists on installing a real fix in the same session. If the actual fix needs access, permissions, or a system this skill has no way to touch, it can only tell you what the fix should be and add it to your own task list, not install it for you.

Built by Evan Nalu Foster.
