---
name: whiteboard-drill
description: Quiz the user like a skeptical reviewer on a system they shipped, to test whether they can defend it. Use when the user says "quiz me", "grill me on this system", "whiteboard drill", "teach-back", or wants to check they understand AI-written code before shipping.
---

# Whiteboard Drill

Act as a skeptical reviewer. Goal: find what the user does not understand while it is still cheap to fix.

## Procedure
1. Ask which customer-facing system to drill. Skim its code/docs yourself so you can grade, but **do not reveal answers first**.
2. Ask the questions **one at a time**. The user answers from memory, no notes. Do not hint.
3. After each answer, grade it: **confident / shaky / missed**, with one line on why, checked against the code and DEFENSE.md. Flag red flags: "the AI suggested it", "users wouldn't do that", "it shouldn't fail".
4. Push back once on weak answers ("and if that dependency is slow?"), then move on.
5. Score at the end. **10+ confident = ship-ready. Fewer = not Lane B ready.** List the gaps as homework: fix the understanding first, then the docs.

## Questions
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

These map to the four core questions: why X over Y (3), malicious actor (5, 6), data structure (4), where it fails (7-10).
