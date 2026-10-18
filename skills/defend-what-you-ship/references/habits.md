# The 25 habits

Each habit: what it is, how to do it, why it matters. Tags show which defense question it serves (Q1 why X/Y, Q2 malicious actor, Q3 data structure, Q4 where it fails).

## Section 1: The Core Five (backbone)

### 1. Handover files (continuity)
Keep a living record the AI reads at the start of every session: what is done, in progress, broken, and to avoid. Not a dump of everything.
- One HANDOVER.md in the repo, newest entry on top.
- Fixed sections: Done, In progress, Broken, Next, Do not touch.
- Tell the AI to read it first and update it last, every session.
Why: every new session starts with amnesia; this is the difference between re-explaining the project and picking up where you left off.

### 2. DECISIONS.md (rationale) · Q1
Log every meaningful decision with reasoning: why this library, pattern, trade-off.
- One entry per decision: context, options, choice, reason, date.
- Have the AI draft the entry before it makes the change, not after.
- Record rejected options; they're the best part.
Why: code shows what changed, DECISIONS shows why. It stops re-arguing settled questions months later.

### 3. Explicit comments (readability)
Require the AI to comment non-obvious logic as it writes: purpose of a block, what calls it, what it assumes.
- Comment intent and assumptions, never syntax.
- Mark invariants (e.g. "must run after auth check").
- Flag surprising code with a WHY note so nobody cleans it up later.
Why: cheap insurance so you or the next AI session understands intent without reverse engineering.

### 4. FLOW.md (traceability) · Q4
Document how execution travels between files, functions, modules: what calls what, in what order, and which part you're changing now.
- Trace entry point to output: file, function, next file, next function.
- Mark the exact functions/lines modified in this change.
- Update when the path changes; a plain text diagram is enough.
Why: bugs live in the gaps between files.

### 5. BUG.md / FEATURE.md (full trace)
One file per bug or feature, traced start to finish.
- Bug: symptom, repro steps, root cause, fix, verification.
- Feature: goal, scope, design, steps, status, open questions.
- Append a timestamped log; never rewrite history.
Why: anyone, human or AI, can read it cold and know how to continue.

## Section 2: Guardrails (control what's allowed before the AI touches a line)

### 6. ARCHITECTURE.md (big picture) · Q1-Q4
High-level map of modules/services and how data moves. Not implementation detail.
- List each module/service and what it owns.
- Show data flow and mark trust boundaries (where outside input enters).
- One page, link to deeper docs.
Why: without a map, every session guesses the terrain; with one the AI can reason about impact before writing.

### 7. CONSTRAINTS.md (boundaries) · Q2
A short, explicit list of what the AI must never do (e.g. don't touch the payment module, always use the repository pattern, no new dependencies without asking).
- Hard rules in plain words: never, always, only.
- Name protected areas: auth, payments, migrations, infra.
- Instruct the AI to stop and ask before breaking any rule.
Why: "allow" should never mean "allow anything"; constraints turn blanket permission into scoped permission.

### 8. Test checklist (verification) · Q4
Concrete list of what to run and check before a change counts as done. Real commands, real expected outputs.
- List exact commands and what a pass looks like.
- Add one manual path a real customer would take.
- Make the AI paste real output instead of saying tests pass.
Why: an AI claiming success and code actually working are different facts.

### 9. ROLLBACK.md (safety net) · Q4
Short plan to undo a change, especially large or risky edits.
- Note the last known good commit/tag before every risky change.
- For data changes, write the down step or backup plan.
- Prefer a feature flag so it can be switched off without a deploy.
Why: confidence to let AI make bigger changes comes from knowing how to reverse them.

## Section 3: Review habits (keep a human in the loop)

### 10. Read the diff (discipline)
Never accept a change based on the AI's summary.
- Scan the changed-file list first; did it touch anything unexpected?
- Hunt for deleted tests, loosened checks, hardcoded values, new network calls.
- If the diff is too big to read, the request was too big.
Why: summaries can be wrong or incomplete; diffs can't lie about what changed.

### 11. Ask why before what (plan first) · Q1
Before implementation, make the AI explain plan and approach.
- Prompt: explain your plan and the alternatives before editing anything.
- Ask: what could go wrong with this plan?
- Approve the plan first, then the code.
Why: far cheaper to correct a flawed plan than unwind a flawed implementation.

### 12. Small requests only (scope control)
One logical change per request, not "fix my whole auth system".
- One behavior change per prompt.
- Commit between steps so each can be reverted alone.
- If you can't name the change in one sentence, split it.
Why: large vague requests produce large vague diffs nobody reviews properly.

## Section 4: Meta habits

### 13. Session handoff summary (ritual)
End every session with a five-line note: what we did, what's left, what to watch out for. Takes 30 seconds.
- Last prompt of the day: summarize in 5 lines: done, left, risks.
- Paste into HANDOVER.md.
- Do it even when tired. Especially then.
Why: cheapest habit on the list, often the highest leverage.

### 14. Version pin your context (traceability)
Note which AI model/version made which decision.
- Put model name and date in each DECISIONS entry.
- Log it when switching models mid-project.
- After a model change, re-verify old assumptions before building on them.
Why: "the AI did this" isn't a full answer once several models touch a project.

### 15. Own the mental model (the real rule) · Q1-Q4
If you can't explain what the code does in your own words, you're not ready to accept it, however thorough the docs.
- Explain the change out loud with no notes.
- Sketch the data flow on paper.
- If you stall, have the AI explain that part, then try again from scratch.
Why: this is the whole point; every file exists to get you to this moment, not excuse you from it.

## Section 5: Defense prep (new in v2)

### 16. DEFENSE.md (capstone) · Q1-Q4
One-page brief per customer-facing system: what it does, how it works, why built that way, how it can be abused, where it breaks.
- Write after the build, before the ship.
- Draft yourself first, let the AI fill gaps, rewrite in your voice.
- Re-read before every release that changes the system.
Why: if you can fill the page without help you pass the benchmark; if not, you've found the gap to close.

### 17. ALTERNATIVES.md (trade-offs) · Q1
For every significant choice, the options rejected and why (a queue not a cron job; Postgres not a document store).
- List two or three real options per major decision.
- Note cost, risk, and what you gave up.
- Add a "revisit if" line: the condition that would change your mind.
Why: without alternatives every choice sounds like the only possible one, which is a red flag.

### 18. THREAT.md (security) · Q2
Who could behave badly and what they could do: anonymous visitor, logged-in user, insider, third-party API, compromised dependency.
- List actors and entry points (forms, APIs, webhooks, file uploads).
- For each, the worst realistic abuse and the mitigation in place.
- Be honest about known gaps.
Why: AI writes code for the happy path; attackers live on every other path.

### 19. FAILURE.md (resilience) · Q4
Map of how the system fails. For each dependency ask: slow, down, wrong, or empty? Note limits: size, scale, concurrency, timeouts.
- Go dependency by dependency: database, APIs, queues, third parties.
- Write the first limit you expect to hit (traffic, payload size, rate limit).
- Note how you'd find out: logs, alerts, dashboards.
Why: "where does this fail?" separates people who understand a system from people who merely deployed it.

### 20. DATA.md (structures) · Q3
Key data structures and schemas, how accessed, how big they get, who may write them.
- For each core structure: shape, access pattern, expected size.
- State the trade-off in one line (e.g. fast lookup, costly ordering).
- Record who writes and who only reads.
Why: the AI picked a structure; you need to know why it was a good pick.

## Section 6: Ship gate hygiene (new in v2)

### 21. Assumptions & open questions (honesty) · Q4
Running list of what you and the AI assume but haven't verified, plus unanswered questions.
- At end of each task ask: what did you assume that I did not tell you?
- Mark each: verified, unverified, or wrong.
- Clear the unverified list before anything ships to customers.
Why: AI fills gaps confidently; writing them down stops confidence passing as knowledge.

### 22. Least-privilege allow policy (permissions) · Q2
Decide in advance what to auto-allow, pause on, and never allow, instead of deciding fresh at every popup while tired.
- Sort actions into three lists: safe, pause and read, never.
- Keep AI tools out of production credentials and live databases.
- Review the allow list when project or risk level changes.
Why: clicking allow is granting access; a written policy makes it a deliberate decision.

### 23. One commit per AI change (git hygiene) · Q4
Commit after every accepted AI change with a message saying what and why.
- Commit before a risky prompt so you can return to it.
- Write messages as intent, not "update".
- Never stack five unrelated AI edits into one commit.
Why: small commits turn a mystery next week into a ten-minute bisect.

### 24. Dependency & secrets log (supply chain) · Q2
Track every dependency the AI adds and every secret/key/credential it touches.
- Record the package, why needed, who maintains it.
- Scan diffs for keys, tokens, `.env` contents before committing.
- Pin versions; prefer fewer, well-known libraries.
Why: every new dependency is code you didn't write and probably won't read; it deserves a reason on file.

### 25. Teach-back drill (practice) · Q1-Q4
Practice the whiteboard before anyone asks: explain the system to a friend, rubber duck, or the AI, then have the AI quiz you with the four questions and grade your answers.
- Prompt: act as a skeptical reviewer and ask me about this system.
- Answer from memory first, then check against DEFENSE.md.
- Where you stumble, fix the understanding, then the docs.
Why: defense is a skill and skills need reps.
