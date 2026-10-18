# Cheat sheets

## Allow, Pause or Never

Decide once, calmly, not at every popup. Adapt to the project.

**Safe to allow**
- Reading files, listing folders
- Running tests and linters
- Formatting code
- Edits on a scratch or PoC branch
- Searching the codebase

**Pause and read**
- Edits across many files
- Config or build changes
- Adding a dependency
- Changing auth or permissions
- Database writes or migrations
- Calls to a new external host
- Deleting files

**Never auto-allow**
- Reading or editing secrets and `.env` files
- Production database or deploy commands
- Force push or history rewrites
- Disabling tests or security checks
- Recursive force deletes
- Piping downloads into a shell
- Payment and auth code without review

Rule of thumb: the harder an action is to undo, the less it deserves a fast click.

## Red flags in a diff

| You see | Ask |
|---|---|
| Tests deleted or skipped | Why is the safety net shrinking? |
| Validation or auth checks loosened | Who benefits from this being easier? |
| New package or network call | Do I know what this is and who runs it? |
| Hardcoded values, keys or URLs | Where should this really live? |
| Huge diff for a small request | What else changed that I did not ask for? |

## The pre-ship gate (run before anything in Lane B goes live)

If you can't tick a box honestly, you're not ready to ship.

- [ ] I can explain how this works at a high level, without notes.
- [ ] DEFENSE.md is written in my own words and is current.
- [ ] I know why we chose this approach over at least one alternative.
- [ ] I can name who could abuse it and what stops them.
- [ ] I know the first place it will fail and how I would notice.
- [ ] I know the main data structures and why they fit.
- [ ] I read the full diff, not just the AI's summary.
- [ ] Tests ran and I saw the real output.
- [ ] A customer path was tried by hand end to end.
- [ ] No secrets, keys or tokens landed in the code.
- [ ] New dependencies are justified and logged.
- [ ] Rollback steps are written and the last good commit is known.
- [ ] Unverified assumptions are cleared or consciously accepted.
- [ ] HANDOVER.md and DECISIONS.md are updated.

## The whiteboard drill (self test)

Pick one customer-facing system. Answer out loud, no notes. Where you hesitate is homework.

1. What does this system do, in two sentences a new teammate would understand?
2. Walk me through one request from entry to response.
3. Why did you choose this approach instead of the obvious alternative?
4. What is the most important data structure here and why does it fit?
5. What is the worst thing an anonymous user could try?
6. What about a logged-in user who is malicious?
7. What happens if your main dependency goes down for an hour?
8. What is the first limit you expect to hit as usage grows?
9. How would you know it broke before a customer told you?
10. How do you undo your last change safely?
11. What did the AI assume that you never verified?
12. What would you change if you had another week?

Score: 10 or more confident answers means you could ship it. Fewer means it is not Lane B ready yet.
