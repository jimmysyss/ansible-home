---
name: code-review
description: Review Ansible YAML files against ansible-home standards
---

# Code Review

Review Ansible roles, playbooks, and variable files against the ansible-home project standards. Follow the checklist in `.github/instructions/code-review.instructions.md`.

## What To Do

1. **Correctness** — Check that every task has a meaningful `name`, uses FQCN, uses YAML dict syntax, and that conditionals are logically sound.
2. **Idempotency** — Identify any tasks that would cause unintended changes on a re-run. Flag `command`/`shell` tasks missing `changed_when`, `creates`, or `removes`.
3. **Security** — Scan for hardcoded passwords, tokens, or private keys. Flag over-broad `become: true` at the play level. Highlight any new open ports needing documentation.
4. **Structure** — Check variable naming conventions, handler naming, role directory layout, and use of `defaults/main.yml` vs `vars/main.yml`.
5. **Testing** — Confirm the change includes a staging validation note and idempotency has been verified.
6. **Lint** — Note any issues that `ansible-lint` would catch, even if the reviewer has not run it yet.

Present findings as a concise list grouped by category with specific line/file references.
