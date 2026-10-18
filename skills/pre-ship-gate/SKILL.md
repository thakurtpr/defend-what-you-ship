---
name: pre-ship-gate
description: Run the 14-item pre-ship checklist before AI-assisted, customer-facing work goes live. Use when the user says "ready to ship?", "pre-ship check", "release gate", or is about to deploy or merge to production. Verifies each item from real evidence and reports blockers.
---

# Pre-Ship Gate

Run before anything customer-facing goes live. If a box can't be ticked honestly, it's a blocker.

For each item: ask the user or verify from evidence (run the command, read the diff, paste real output). Never accept "tests pass" without output. **Never tick the understanding items yourself**; those are the user's to confirm.

- [ ] I can explain how this works at a high level, without notes. *(user only)*
- [ ] DEFENSE.md is written in my own words and is current. *(user only)*
- [ ] I know why we chose this approach over at least one alternative. *(check DECISIONS/ALTERNATIVES)*
- [ ] I can name who could abuse it and what stops them. *(check THREAT)*
- [ ] I know the first place it will fail and how I would notice. *(check FAILURE)*
- [ ] I know the main data structures and why they fit. *(check DATA)*
- [ ] I read the full diff, not just the AI's summary. *(offer to walk the diff)*
- [ ] Tests ran and I saw the real output. *(run them)*
- [ ] A customer path was tried by hand end to end.
- [ ] No secrets, keys or tokens landed in the code. *(scan the diff and `.env`)*
- [ ] New dependencies are justified and logged. *(diff manifests vs log)*
- [ ] Rollback steps are written and the last good commit is known. *(check ROLLBACK, `git log`)*
- [ ] Unverified assumptions are cleared or consciously accepted. *(check ASSUMPTIONS)*
- [ ] HANDOVER.md and DECISIONS.md are updated.

## Output
A table: item, status (pass / fail / needs user), evidence. End with **SHIP** only if every item passes; otherwise **BLOCKED** plus the shortest path to clear each blocker. If DEFENSE.md is missing, suggest the `defend-what-you-ship` skill; to practice, suggest `whiteboard-drill`.
