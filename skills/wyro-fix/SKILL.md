---
name: wyro-fix
description: Fix what the Wyro architecture check found, most dangerous first, re-checking after each fix until CI would pass. Use when the user asks to fix Wyro findings, secure unauthenticated routes, or make the Wyro gate pass.
---

# Fix Wyro findings

1. Run the check from the backend's root:

   ```bash
   npx -y wyro-check@latest . --no-interactive --json
   ```

2. Take the most dangerous NEW finding (highest risk, highest confidence). Read the route's handler and the code around it before changing anything.
3. Fix it the way the codebase already does it: reuse the project's existing auth middleware, guard or session check, and scope queries to the caller where the finding asks for it. Do not invent a new auth system.
4. Run the check again. Confirm the finding is gone and nothing new appeared.
5. Repeat until the check passes, or until the remaining findings are ones the user says are intended.

## Rules

- Never edit `.wyro/baseline.json` or `wyro.json`, and never run `--update-baseline`, to make a finding go away. If a finding is intended (for example a public catalogue), stop and ask the user; recording it as known debt is their decision.
- Keep each fix small and tell the user what changed and why, with the file and line.
- If the check exits with code `2`, nothing could be read: say so instead of claiming success.
