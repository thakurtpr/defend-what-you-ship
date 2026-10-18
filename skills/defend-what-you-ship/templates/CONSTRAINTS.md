# CONSTRAINTS
The AI must stop and ask before breaking any rule below.

Never:
- touch <protected area: auth / payments / migrations / infra>
- add a dependency without asking
- read or edit .env or secrets
- disable or delete tests to make a change pass

Always:
- follow <pattern, e.g. repository pattern>
- explain the plan and alternatives before editing
- paste real command output when claiming tests pass

Only:
- <what is allowed in sensitive areas>
