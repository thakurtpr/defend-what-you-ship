# Folder layout and 7-day plan

```
docs/
  HANDOVER.md       where things stand
  DECISIONS.md      what we chose and why
  ALTERNATIVES.md   what we rejected
  ARCHITECTURE.md   the system map
  FLOW.md           how execution travels
  CONSTRAINTS.md    what is off limits
  THREAT.md         who could abuse it
  FAILURE.md        where it breaks
  DATA.md           structures and schemas
  TESTING.md        how we verify
  ROLLBACK.md       the way back out
  features/         FEATURE-001.md ...
  bugs/             BUG-001.md ...
  defense/          one DEFENSE brief per shipped system
```

## 7-day plan

| Day | Focus |
|---|---|
| 1 | **Handover and Constraints.** Create HANDOVER.md and CONSTRAINTS.md. Tell the AI to read them first. |
| 2 | **Architecture and Flow.** Draw the system map and trace one real request through it. |
| 3 | **Decisions habit.** Ask the AI to draft a Decisions entry before every non-trivial change. |
| 4 | **Test and Rollback.** Write the checklist and note the last known good commit. |
| 5 | **Threat and Failure.** Spend an hour being your own attacker, then your own outage. |
| 6 | **Data and Alternatives.** Document core structures and the options you turned down. |
| 7 | **First whiteboard.** Explain a shipped system to a friend and have them ask the four questions. |
