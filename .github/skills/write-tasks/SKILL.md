---
name: write-tasks
description: Write idiomatic, idempotent Ansible tasks for a given goal
---

# Write Tasks

Generate idiomatic Ansible task YAML for a described goal, following ansible-home project conventions. Always apply the patterns from `../../copilot-instructions.md`.

## What To Do

1. Use `ansible.builtin.*` FQCN for all built-in modules.
2. Write task `name` fields as descriptive Title Case sentences describing the desired outcome.
3. Use YAML dict syntax for all task arguments — never inline `key=value` style.
4. Ensure every generated task is idempotent: running it a second time must produce `ok`, not `changed`.
5. Add a `when:` guard if the task is conditional on a variable (e.g., `with_gui`, `ansible_os_family`).
6. Apply relevant tags from the project standard set: `packages`, `config`, `service`, `files`, `security`.
7. Wrap related tasks in `block:` / `rescue:` when there is a meaningful error-handling story.
8. For `command`/`shell` tasks, always add `changed_when`, `creates`, or `removes` to preserve idempotency.
9. Notify the appropriate handler (e.g., `restart nginx`) instead of restarting services inline.
