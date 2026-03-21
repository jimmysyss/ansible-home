---
name: refactor-code
description: Refactor existing Ansible roles or tasks to improve clarity, idempotency, or standards compliance
---

# Refactor Code

Improve existing Ansible YAML without changing the intended behaviour. Always preserve idempotency and follow `../../copilot-instructions.md`.

## What To Do

1. **Upgrade module references** — Replace bare module names with FQCN equivalents (e.g., `apt` → `ansible.builtin.apt`).
2. **Fix task style** — Convert any inline `key=value` task arguments to YAML dict syntax.
3. **Improve names** — Rewrite vague task `name` fields into clear, outcome-oriented Title Case sentences.
4. **Flatten large task files** — Break a `tasks/main.yml` with more than ~30 tasks into focused sub-task files imported via `include_tasks`.
5. **Centralise variables** — Move hardcoded values into `defaults/main.yml` with appropriate comments.
6. **Fix idempotency gaps** — Add `changed_when: false` or appropriate guards to `command`/`shell` tasks.
7. **Add handlers** — Replace inline service restarts with `notify` + handler pattern.
8. **Apply tags** — Add missing `packages`, `config`, `service`, `files`, `security` tags.

Explain each refactoring change and why it improves quality or compliance.
