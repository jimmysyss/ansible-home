---
name: setup-role
description: Scaffold a new Ansible role with the standard directory structure for this project
---

# Setup Role

Scaffold a new Ansible role following the ansible-home project conventions. Always follow the patterns established in `../../copilot-instructions.md`.

## What To Do

1. Create the standard role directory structure under `roles/<role-name>/`:
   - `tasks/main.yml` — entry-point that uses `include_tasks` to delegate to sub-task files
   - `handlers/main.yml` — service restart/reload handlers
   - `defaults/main.yml` — user-overridable variables with sensible defaults and comments
   - `vars/main.yml` — internal constants (use sparingly)
   - `files/` — static files to copy to managed hosts
   - `templates/` — Jinja2 templates (`.j2` extension)
   - `meta/main.yml` — role metadata and Galaxy dependencies
   - `README.md` — role description, variables table, and usage example

2. Pre-populate each file with the correct YAML header and a brief comment describing its purpose.

3. Prefix all role-specific variable names with the role name (e.g., `nginx_port` for the `nginx` role).

4. Apply `ansible.builtin.*` FQCN references in all generated task stubs.

5. Add appropriate tags (`packages`, `config`, `service`, `files`) to task stubs.
