---
name: defend-what-you-ship
description: Keeps AI-assisted coding defensible. Use when building or changing customer-facing code with AI, before shipping, when the user says "defend this", "whiteboard defense", "pre-ship gate", "am I ready to ship", "set up handover/decisions docs", "allow policy", or asks to be quizzed on their own system. Sets up the doc trail (HANDOVER, DECISIONS, THREAT, FAILURE...), runs the pre-ship checklist, and drills the four defense questions.
---

# Defend What You Ship

**Benchmark (the Whiteboard Defense):** at any moment someone can pull the user aside and ask them to explain any customer-facing system they shipped, how it works, and defend the decisions behind it. Not line-level recall. A clear high-level explanation, the reasons behind decisions, and honest answers on where it breaks and how it could be abused.

Core rule: **a blind "allow" is not a decision.** Fast is easy; owning it is hard. Write things down and be able to explain what ships.

Adapted from the *Defend What You Ship: AI Field Guide v2 (Whiteboard Edition)*.

## Step 0: Pick the lane

Ask once: **"If this broke tonight, would a customer notice or be harmed?"**

| | Lane A: PoC / demo / experiment | Lane B: customer-facing |
|---|---|---|
| Goal | Learn fast, throw away | Serve real people safely |
| Priority | Speed over quality | Correctness, safety, clarity |
| Understanding | None required | High-level, defensible at a whiteboard |
| Docs | None | Core files + DEFENSE.md + pre-ship gate |

- **Lane A:** do not add process. Generate freely and stay out of the way.
- **Lane B:** apply everything below.
- **Promotion rule:** the moment a PoC gets a real user it becomes Lane B, and any code generated but never understood needs its defense written before it stays live.

## The four defense questions

Every Lane B system must survive these. Each maps to files that back the answer up.

| Question | Good answer includes | Red flag | Back-up files |
|---|---|---|---|
| 1. "Why X instead of Y?" | Options considered, cost of each, why this won here | "The AI suggested it" (a source, not a reason) | DECISIONS, ALTERNATIVES |
| 2. "What if an actor is malicious?" | Actors, what they can reach/send/abuse, controls (validation, auth, rate limits, least privilege) | "Users wouldn't do that" | THREAT, CONSTRAINTS, ARCHITECTURE |
| 3. "What data structure and why?" | Shape, read/write pattern, max size, trade-off | Not knowing it exists or why it fits | DATA, FLOW |
| 4. "Where does this fail?" | First limit you'll hit, what happens when a dependency is slow/down, how you'd notice | "It shouldn't fail" | FAILURE, TESTING, ROLLBACK |

## Workflows

Pick the one matching the request. Templates live in `templates/`; full habit details in `references/habits.md`.

### A. Set up (new or existing Lane B project)
1. Create `docs/` with the layout in `references/layout-and-plan.md` (copy files from `templates/`; don't overwrite existing ones).
2. Always start with HANDOVER.md and CONSTRAINTS.md. Add the rest as the project needs them (7-day plan in the layout reference).
3. Add a line to the project's CLAUDE.md/AGENTS.md: *read docs/HANDOVER.md and docs/CONSTRAINTS.md first; update HANDOVER.md last; draft a DECISIONS entry before any non-trivial change.*

### B. During work (every AI change)
- Read HANDOVER.md and CONSTRAINTS.md at session start; stop and ask before breaking a constraint.
- **Plan before code:** explain the plan, alternatives, and what could go wrong; get approval, then edit.
- **Small requests:** one logical change per request; if it can't be named in one sentence, split it.
- Draft a DECISIONS entry (with model name + date) before a non-trivial change; record rejected options.
- Comment intent, assumptions, and invariants, never syntax.
- **Commit after each accepted change**, message states what and why. Commit before risky prompts.
- Record every new dependency (what, why, maintainer, pinned version) and scan diffs for keys, tokens, `.env` content.
- End of task: list what was assumed but not verified (mark verified / unverified / wrong).
- End of session: 5-line handoff (done, left, risks) pasted into HANDOVER.md.

### C. Review a diff
Never trust the summary; read the real diff. Check the changed-file list first, then scan for the red flags in `references/cheatsheets.md` (deleted/skipped tests, loosened auth/validation, new package or network call, hardcoded values, huge diff for a small ask). If the diff is too big to read, the request was too big.

### D. Pre-ship gate
Run the 14-item checklist in `references/cheatsheets.md`. For each box, ask the user or verify from evidence (paste real command output, never "tests pass"). Report unticked boxes as blockers. If DEFENSE.md is missing or stale, offer workflow E. Do not tick boxes on the user's behalf for understanding-based items.

### E. Write DEFENSE.md
Use `templates/DEFENSE.md`. The user drafts first, in their own words; you fill gaps and flag things you inferred; the user rewrites in their voice. This is the whiteboard cheat sheet, so never present AI-authored text as the user's understanding without them confirming it.

### F. Teach-back drill
Act as a skeptical reviewer. Ask the 12 whiteboard-drill questions (`references/cheatsheets.md`) one at a time about a chosen system. The user answers from memory first; only then check against DEFENSE.md and the code and grade. Score: **10 or more confident answers = ship-ready; fewer = not Lane B ready.** Where they stumble, fix the understanding first, then the docs.

### G. Allow policy
Help the user decide in advance, calmly, what to auto-allow, pause on, and never allow (lists in `references/cheatsheets.md`; adapt to the project). Rule of thumb: the harder an action is to undo, the less it deserves a fast click. Offer to encode it in the tool's permission settings, but only change settings when the user asks.

## Principles to hold yourself to
- Docs support understanding; they never replace it. If the user can't explain the change in their own words, they aren't ready to accept it (habit 15, "the real rule").
- Append timestamped logs; never rewrite history in BUG/FEATURE files.
- Admit known gaps in writing; an admitted gap beats a hidden one.
- Be honest about verification: say what you ran and what you did not.
