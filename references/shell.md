# Shell and Bash Scripts

Honor the requested shell and the project's supported platforms. Declare the intended interpreter with an appropriate shebang and do not claim POSIX compatibility when using Bash-specific features.

Quote expansions, handle spaces and newlines in paths, avoid unsafe command construction and `eval`, and use arrays where Bash argument boundaries matter. Apply strict-mode options only when their behavior is understood for the script's pipelines, conditionals, and cleanup. Use traps for temporary-resource cleanup when appropriate, preserve meaningful exit codes, and send diagnostics to stderr.

Resolve destructive targets to bounded paths before acting. Reject empty, root, home, workspace-root, or otherwise overbroad targets. Provide a faithful dry-run when feasible. For material deletion, replacement, permission, service, or system-configuration changes, create a separate rollback script; if complete restoration is impossible, document partial recovery and the manual procedure.

The manual must name the supported shells and operating systems, required commands and versions, environment variables, permissions, working directory, path assumptions, exit codes, and complete invocation examples. Explain representative success and likely failure output.

Validate with the target shell's syntax check and use `shellcheck` when available and appropriate. Exercise filesystem mutations only in an isolated temporary tree unless the real target has been explicitly authorized.
