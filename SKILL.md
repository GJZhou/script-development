---
name: script-development
description: Create, modify, debug, review, or validate Python, SQL/database, and Shell/Bash scripts when the script is the primary deliverable. Require a matching operation manual and, for material side effects, recovery artifacts. Do not use for ordinary application development, syntax-only explanations, architecture design, or deployment work.
---

# Script Development

Deliver maintainable scripts together with the operational information needed to run, verify, and recover them safely.

## Establish the Contract

Inspect the repository before choosing names, locations, runtimes, database dialects, or conventions. Preserve established project structure. If none exists, place each deliverable in `scripts/<script-name>/`; use the same base name for the primary script and its Markdown manual, and suffix companion scripts with `-rollback`, `-backup`, or `-validate`.

Determine the script's exact inputs, outputs, execution target, scope, dependencies, success criteria, likely failure modes, and side effects. Ask only when a material choice cannot be derived safely. For SQL, identify the database engine and version from project configuration; ask when dialect or transaction behavior remains ambiguous.

Read only the relevant guide:

- Python: [references/python.md](references/python.md)
- SQL and database changes: [references/database.md](references/database.md)
- POSIX Shell or Bash: [references/shell.md](references/shell.md)

PowerShell may be recognized as the active environment, but do not silently translate a requested POSIX Shell/Bash deliverable into PowerShell.

## Deliver the Script Package

Create or update one Markdown operation manual whose base name matches the primary script. Keep the manual synchronized whenever behavior, parameters, names, order, or recovery changes. The single manual must cover the primary script and every companion script.

The manual must state:

1. Purpose, intended use, and explicitly excluded operations.
2. Every input, output, argument, environment variable, and configurable value, with interpreted input and output examples.
3. Invocation, execution order, working directory, dependencies, and complete runnable command examples.
4. Normal results, observable correctness criteria, and an explanation of representative successful output.
5. Likely exceptions, representative error output, resulting state, and practical handling.
6. Real execution constraints such as permissions, supported versions, expected data state, capacity, and platform.
7. For database scripts, the exact database, schema, table, partition, time window, predicate, or other execution scope. Enumerate and demonstrate every configurable scope value.
8. For rollback, backup, and validation companions: purpose, timing, invocation, scope, dependencies, results, and success criteria.

Examples must match the real filenames and implemented interface. Do not present a partial or non-runnable placeholder as a complete command. Mark secrets with explicit safe placeholders such as `<DB_PASSWORD>` and never embed real credentials.

## Manage Side Effects and Recovery

Treat database writes, bulk file deletion or replacement, and system-configuration changes as material side effects. Such a primary script must have a separate rollback script. Design backup and validation companions according to the database rules in the database guide.

The manual must distinguish fully recoverable, partially recoverable, and unrecoverable effects. For rollback, document prerequisites, affected scope, observable success conditions, residual state, risks, and manual recovery steps for anything automation cannot restore. Never describe an unverified or partial recovery as complete.

Before running material side effects, resolve the exact target and scope and disclose recovery limitations. Prefer syntax checks, static analysis, dry runs, temporary directories, test databases, read-only checks, or rollback-capable transactions. Obtain the authorization required by the current environment immediately before a real write or system-level mutation.

## Quality and Verification

Use clear parameters, meaningful logs, reliable exit codes, robust error handling, and proportionate tests. Follow existing project tooling; avoid heavyweight frameworks for a simple script. Preserve unrelated user changes.

Verify the script and manual together:

- Run appropriate syntax and static checks.
- Exercise representative success and common failure cases safely.
- Confirm documented commands, parameters, outputs, execution order, and filenames match the implementation.
- Verify rollback and backup artifacts against isolated or test data where feasible.
- Verify validation logic demonstrates the stated success conditions rather than only checking process exit status.

If modifying an existing script, also update its manual and every affected recovery, backup, or validation companion. Do not claim completion while required documentation or recovery artifacts are missing.
