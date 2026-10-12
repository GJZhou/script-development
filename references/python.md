# Python Scripts

Use the project's supported Python version, dependency manager, formatter, linter, and test runner when present. Otherwise prefer the standard library and state the minimum supported Python version.

For command-line scripts, use explicit arguments, useful `--help`, stable output, meaningful stderr messages, and nonzero exit codes for failure. Avoid hidden interactive prompts unless interaction is part of the request. Validate external paths and inputs before mutation; make destructive scope visible and offer a dry run when it can faithfully preview the action.

Separate operational logic from argument parsing when that materially improves testing. Add type annotations, structured functions, logging, and tests in proportion to complexity. Do not log credentials or sensitive record contents.

In the manual, reproduce the actual help contract: arguments, defaults, environment variables, input formats, output destinations, exit behavior, and at least one realistic success and common-failure example. If the script mutates files or system state materially, provide a separate rollback script and document both automated and manual recovery.

Validate with compilation or import checks and focused tests. Run mutation scenarios only in an isolated temporary location or against disposable fixtures unless the user has authorized the real target.
