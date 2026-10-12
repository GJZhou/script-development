# Database Scripts

## Dialect and Execution Scope

Determine the database engine and version before writing dialect-sensitive SQL. Preserve the project's migration tool, transaction model, naming, statement delimiters, and deployment conventions. Do not assume that DDL is transactional or that rollback semantics are portable.

Every database manual must name the target database, schema, objects, and affected row or partition scope. Explain predicates, time windows, tenant identifiers, batch sizes, and other configurable limits with concrete examples. Include preview or count queries where they give operators a trustworthy view of the affected set.

## Companion Decision Rules

A database script that performs writes or structural changes requires a separate rollback script.

Also require a backup script when the change overwrites or deletes irreplaceable data, performs destructive structural changes, or alters data that cannot be reconstructed reliably from an authoritative source. The backup script and manual must define the exact objects and rows captured, destination and format, retention assumptions, integrity checks, and relationship to restoration.

Require a validation script for migrations, bulk updates, constraints, or structural changes when a successful process exit cannot prove the intended state. Validation should be read-only when possible and must encode observable success conditions such as expected counts, absence of invalid rows, schema properties, referential consistency, or reconciled aggregates.

## Recovery Contract

The rollback script must target the same bounded scope as the primary change and must avoid undoing unrelated later changes. Where exact restoration is impossible, provide the best safe partial recovery, clearly enumerate remaining effects and risks, and document executable manual recovery steps. Do not label partial recovery as complete.

The shared manual must specify execution order, transaction and locking behavior, expected duration or load when knowable, permissions, prerequisites, idempotency or rerun behavior, failure state, and success criteria for primary, backup, validation, and rollback scripts.

## Verification

Prefer parsing or dry-run facilities supplied by the actual database tool, isolated databases, snapshots, read-only previews, or rollback-capable test transactions. Verify that backup scope covers the stated recovery need, rollback restores the promised state, and validation fails on representative incorrect states. Never treat exit status alone as proof of data correctness when state-based checks are required.
