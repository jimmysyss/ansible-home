---
name: debug-issue
description: Diagnose and fix failing Ansible playbook runs in the ansible-home project
---

# Debug Issue

Systematically investigate and resolve Ansible failures in the ansible-home project. Follow the conventions in `../../copilot-instructions.md`.

## What To Do

1. **Collect context** — Ask for (or read) the full error output, the failing task name, and the playbook/role file where it occurs.
2. **Identify the error class** — Categorise the failure:
   - Connection/SSH error (unreachable host, wrong key, wrong user)
   - Module failure (wrong arguments, missing dependency, permission denied)
   - Variable undefined or wrong type
   - Template rendering error (Jinja2 syntax, undefined variable)
   - Idempotency violation (unexpected `changed` on second run)
   - Handler not triggered or triggered too early
3. **Suggest targeted fixes** — Provide the minimal change to resolve the issue without unnecessary refactoring.
4. **Verify idempotency** — After suggesting the fix, remind the user to rerun with `--check --diff` and then perform a second live run to confirm zero `changed` tasks.
5. **Prevent regression** — Suggest an `ansible-lint` rule or task guard that would catch this class of error in the future.

When in doubt, ask for the output of `ansible-playbook -vvv` to get detailed SSH and module debug information.
