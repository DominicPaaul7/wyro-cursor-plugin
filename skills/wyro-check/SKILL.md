---
name: wyro-check
description: Check a backend's architecture with Wyro and fix what it finds. Use after changing routes, handlers, middleware or schema, before opening a pull request, or when asked whether a backend is safe to ship.
---

# Wyro architecture check

Wyro reads a backend's source and reports which routes reach which tables, and which do so without authenticating, validating input or rate limiting. It is deterministic: the same code always gets the same answer.

## Steps

1. Call the `check_backend` tool on the backend's root directory.
2. Show Wyro's verdict card exactly as returned, then at most the top three NEW findings with their file and line.
3. Fix the most dangerous real finding. Check again. Repeat until CI would pass, or until the remaining findings are ones the user says are intended.
4. Never edit `.wyro/baseline.json` or `wyro.json` to silence a finding.

## Other tools

- `describe_backend`: every route (method, path, file:line), whether it authenticates, and the tables it reads or writes. Use it before changing a codebase you do not know.
- `list_rules`: every rule the check applies and what it protects against.

Reads TypeScript, JavaScript, Python and SAP CAP: Express, NestJS, Next.js, FastAPI, Prisma, Drizzle, TypeORM, Mongoose, SQLAlchemy and Supabase.
