# defend-what-you-ship

Agent skills that keep AI-assisted code **defensible**. Works with Claude Code, Antigravity, Cursor, Codex, Copilot, Gemini CLI, Windsurf, OpenCode and 70+ other agents.

> I should be able to pull you aside at any moment and ask you to explain any customer-facing system you have shipped, how it works, and defend the decisions you made.

## Install (one line)

```bash
npx skills add thakurtpr/defend-what-you-ship
```

Uses the open [skills CLI](https://skills.sh) and auto-detects your installed agents. Useful flags:

```bash
npx skills add thakurtpr/defend-what-you-ship -g                      # global, all projects
npx skills add thakurtpr/defend-what-you-ship -a claude-code          # one agent
npx skills add thakurtpr/defend-what-you-ship -a antigravity          # Antigravity
npx skills add thakurtpr/defend-what-you-ship -s pre-ship-gate        # one skill only
npx skills add thakurtpr/defend-what-you-ship --all -y                # everything, no prompts
```

**Claude Code plugin** (auto-updates):

```bash
claude plugin marketplace add thakurtpr/defend-what-you-ship
claude plugin install defend-what-you-ship@defend-what-you-ship
```

**Manual:** copy any folder under `skills/` into your agent's skills directory.

| Agent | Project | Global |
|---|---|---|
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| Antigravity | `.agents/skills/` | `~/.gemini/antigravity/skills/` |
| Cursor, Gemini CLI, OpenCode | `.agents/skills/` | see the [skills CLI](https://github.com/vercel-labs/skills) |

## The skills

Small and independent: install one or all.

| Skill | Use it to |
|---|---|
| `defend-what-you-ship` | Pick the lane (PoC vs customer-facing), set up the `docs/` trail, follow the per-change rules, review diffs, write DEFENSE.md |
| `pre-ship-gate` | Run the 14-item checklist before anything goes live; verified from evidence, reports blockers |
| `whiteboard-drill` | Get quizzed by a skeptical reviewer on a system you shipped; scored out of 12 |
| `allow-policy` | Decide what an agent may auto-run, must pause on, and never do |

Ask in plain language ("run the pre-ship gate", "quiz me on this system", "set up handover docs") or invoke by name, e.g. `/pre-ship-gate`.

## The idea in 30 seconds
- **Two lanes:** if it broke tonight, would a customer notice? No: move fast. Yes: be ready to defend it.
- **Four questions:** why X over Y; what if an actor is malicious; what data structure and why; where does it fail.
- **Paper trail:** HANDOVER, DECISIONS, ALTERNATIVES, CONSTRAINTS, THREAT, FAILURE, DATA, ROLLBACK, DEFENSE. Starter files in `skills/defend-what-you-ship/templates/`.
- **Never accept a summary:** read the diff, see real test output, own the mental model.

## Layout
```
skills/
  defend-what-you-ship/   SKILL.md, references/ (25 habits, cheat sheets, 7-day plan), templates/
  pre-ship-gate/SKILL.md
  whiteboard-drill/SKILL.md
  allow-policy/SKILL.md
.claude-plugin/           plugin + marketplace manifests
AGENTS.md
```

## Credits
Adapted from *Defend What You Ship: AI Field Guide v2 (Whiteboard Edition)*. This is a condensed, restructured adaptation for agent use; see the original for the full text. Issues and PRs welcome.

## License
MIT
