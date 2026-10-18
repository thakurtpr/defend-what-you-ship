---
name: allow-policy
description: Write a least-privilege allow policy for an AI coding tool, deciding in advance what to auto-allow, pause on, and never allow. Use when the user asks about permissions, "stop clicking allow", auto-approve settings, or what an agent should be allowed to run.
---

# Allow Policy

A click on "allow" grants access. Decide once, calmly, instead of at every popup while rushing. Rule of thumb: **the harder an action is to undo, the less it deserves a fast click.**

## Default lists (adapt to the project)
**Safe to allow:** read files, list folders, run tests and linters, format code, edits on a scratch/PoC branch, search the codebase.

**Pause and read:** edits across many files, config/build changes, adding a dependency, auth or permission changes, database writes or migrations, calls to a new external host, deleting files.

**Never auto-allow:** reading or editing secrets and `.env`; production database or deploy commands; force push or history rewrites; disabling tests or security checks; recursive force deletes; piping downloads into a shell; payment and auth code without review.

## Procedure
1. Look at the project (stack, scripts, deploy path, where secrets live) and tailor the three lists, naming real commands and paths.
2. Keep AI tools away from production credentials and live databases.
3. Write the policy to `docs/CONSTRAINTS.md` (or the repo's agent instructions).
4. Offer to encode it in the tool's permission settings, but **only change settings if the user asks**.
5. Remind them to revisit it when the project or risk level changes.
