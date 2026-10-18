---
name: defend-what-you-ship
description: Set up and follow the doc trail that keeps AI-written, customer-facing code defensible (HANDOVER, DECISIONS, CONSTRAINTS, THREAT, FAILURE, DEFENSE). Use when starting or changing code with AI, setting up handover/decisions docs, reviewing an AI diff, or when asked "can I defend this". Sibling skills handle the pre-ship gate, the quiz drill, and the allow policy.
---

# Defend What You Ship

**Benchmark:** someone can pull the user aside at any moment and ask them to explain any customer-facing system they shipped and defend its decisions. Not line-level recall: a clear high-level explanation, the reasons behind choices, and honest answers on where it breaks and how it could be abused.

A blind "allow" is not a decision. Write things down; be able to explain what ships.

Related skills (install the whole repo for all): `pre-ship-gate`, `whiteboard-drill`, `allow-policy`.

## Step 0: Pick the lane
Ask once: **"If this broke tonight, would a customer notice or be harmed?"**
- **No → Lane A (PoC/demo):** generate freely, add no process, stay out of the way.
- **Yes → Lane B (customer-facing):** apply everything below.
- **Promotion rule:** the moment a PoC gets a real user it is Lane B, and code that was generated but never understood needs its defense written before it stays live.

## The four questions every Lane B system must survive
| Question | Good answer | Red flag | Backed by |
|---|---|---|---|
| Why X instead of Y? | Options, their costs, why this one won here | "The AI suggested it" | DECISIONS, ALTERNATIVES |
| What if an actor is malicious? | Actors, reach, abuse, controls | "Users wouldn't do that" | THREAT, CONSTRAINTS, ARCHITECTURE |
| What data structure and why? | Shape, access pattern, size, trade-off | Not knowing why it fits | DATA, FLOW |
| Where does this fail? | First limit, dependency down/slow, how you'd notice | "It shouldn't fail" | FAILURE, TESTING, ROLLBACK |

## A. Set up docs (once per Lane B repo)
1. Create `docs/` per `references/layout-and-plan.md`, copying from `templates/`. Never overwrite existing files.
2. Start with HANDOVER.md and CONSTRAINTS.md; add others as needed.
3. Add to the repo's CLAUDE.md / AGENTS.md: *Read docs/HANDOVER.md and docs/CONSTRAINTS.md first. Update HANDOVER.md last. Draft a DECISIONS entry before any non-trivial change.*

## B. During every AI change
- Read HANDOVER + CONSTRAINTS at session start; stop and ask before breaking a constraint.
- **Plan first:** state plan, alternatives, and what could go wrong; get approval before editing.
- **One logical change per request.** If it can't be named in one sentence, split it.
- Draft a DECISIONS entry (model + date, rejected options) before non-trivial changes.
- Comment intent, assumptions and invariants, never syntax.
- **Commit after each accepted change** (what and why); commit before risky steps.
- Log new dependencies (what, why, maintainer, pinned version); scan diffs for keys, tokens, `.env` content.
- End of task: list assumptions not verified (verified / unverified / wrong).
- End of session: 5-line handoff (done, left, risks) into HANDOVER.md.

## C. Review a diff
Never trust the summary. Read the changed-file list, then the diff. Red flags: tests deleted or skipped; auth/validation loosened; new package or network call; hardcoded values, keys or URLs; huge diff for a small ask (the request was too big). Full table in `references/cheatsheets.md`.

## D. Write DEFENSE.md
Use `templates/DEFENSE.md`. The user drafts first in their own words; fill gaps, mark what you inferred, and have them rewrite it in their voice. Never present AI-authored text as the user's understanding without their confirmation.

## Rules for you
- Docs support understanding, they never replace it. If the user can't explain the change in their own words, they aren't ready to accept it.
- Append timestamped logs; never rewrite history in BUG/FEATURE files.
- Admit known gaps in writing. Say what you ran and what you did not.

Deeper detail: `references/habits.md` (all 25 habits), `references/cheatsheets.md`.
