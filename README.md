# defend-what-you-ship

An agent skill for AI-assisted coding that keeps you able to **explain and defend what you ship**.

> I should be able to pull you aside at any moment and ask you to explain any customer-facing system you have shipped, how it works, and defend the decisions you made.

Every "allow" click is a decision. This skill gives your AI assistant the paper trail, guardrails, and benchmark to make it an informed one.

## What it does
- **Picks the lane**: PoC (move fast, no process) vs customer-facing (full defense).
- **Sets up `docs/`**: HANDOVER, DECISIONS, ALTERNATIVES, ARCHITECTURE, FLOW, CONSTRAINTS, THREAT, FAILURE, DATA, TESTING, ROLLBACK, plus BUG/FEATURE traces.
- **Guides every AI change**: plan before code, small requests, decision log, commit per change, dependency/secrets log.
- **Reviews diffs** against a red-flag list.
- **Runs the 14-item pre-ship gate.**
- **Drills you** on the four questions (why X over Y, malicious actor, data structure, where it fails) with a 12-question teach-back and a ship-ready score.
- **Helps write a least-privilege allow policy** (allow / pause / never).

## Install

Claude Code (user-level, available in every project):

```bash
git clone https://github.com/thakurtpr/defend-what-you-ship.git
mkdir -p ~/.claude/skills
cp -R defend-what-you-ship/skills/defend-what-you-ship ~/.claude/skills/
```

Project-level: copy `skills/defend-what-you-ship` into `<your-repo>/.claude/skills/`.

Other agents that read `SKILL.md`-style skills: copy the same folder into that tool's skills directory.

## Use
Ask in natural language, or invoke the skill by name:
- "Set up the defend-what-you-ship docs for this repo"
- "Run the pre-ship gate on this feature"
- "Quiz me on this system (teach-back drill)"
- "Review this diff for red flags"
- "Help me write an allow policy"

## Layout
```
skills/defend-what-you-ship/
  SKILL.md                      workflows and rules
  references/habits.md          the 25 habits
  references/cheatsheets.md     allow/pause/never, diff red flags, pre-ship gate, drill
  references/layout-and-plan.md docs/ layout and 7-day adoption plan
  templates/                    copy-paste starter files
```

## Credits
Adapted from *Defend What You Ship: AI Field Guide v2 (Whiteboard Edition)*. Content here is a condensed, restructured adaptation for agent use; see the original guide for the full text and design. Contributions welcome via issues and PRs.

## License
MIT
