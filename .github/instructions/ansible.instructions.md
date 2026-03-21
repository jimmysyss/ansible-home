---
applyTo: "**/*.yml,**/*.yaml,**/*.j2"
description: "Ansible development standards for the ansible-home project"
---

# Ansible Coding Standards

Apply the repository-wide guidance from `../copilot-instructions.md` to all Ansible code.

## General Guidelines
- Write all Ansible code to be idempotent — running the same playbook multiple times must produce the same result.
- Prefer declarative state descriptions over procedural commands; use the appropriate Ansible module rather than `ansible.builtin.shell` or `ansible.builtin.command`.
- Always use fully-qualified collection names (FQCN) for all modules (e.g., `ansible.builtin.apt`, not just `apt`).

## Task Style
- Use YAML dictionary syntax for all task arguments — never use the inline `key=value` format.
- Every task must have a clear, human-readable `name` in Title Case that describes the outcome.
- Group related tasks into `block:` structures and always pair them with `rescue:` when failures need handling.
- Apply tags consistently across roles: `packages`, `config`, `service`, `files`, `security`.

## Variables
- Declare all user-overridable variables with sensible defaults in `defaults/main.yml`.
- Reserve `vars/main.yml` for internal constants that must not be overridden.
- Prefix role-specific variables with the role name (e.g., `nginx_port`, `common_packages`).
- Use `group_vars/` for inventory-group defaults and `host_vars/` only for true per-host exceptions.
- Avoid hard-coding sensitive values; reference vault-encrypted variables or environment-specific group vars.

## Role Structure
- Each role must follow the standard layout: `tasks/`, `handlers/`, `defaults/`, `vars/`, `files/`, `templates/`, `meta/`.
- Keep `tasks/main.yml` as a thin orchestrator that uses `include_tasks` to delegate to focused sub-task files.
- All Jinja2 templates must have the `.j2` extension and live in `templates/`.
- Handlers must use descriptive `snake_case` names that read as verbs (e.g., `restart nginx`, `reload systemd`).

## Inventory & Host Targeting
- Always test against `inventory/staging` before applying to `inventory/production`.
- Use `--limit` to target specific groups or hosts during development.
- Prefer group membership over per-host variables for anything that applies to more than one host.

## Security Hygiene
- Never commit plaintext passwords or private keys; use `ansible-vault` for secrets.
- Limit privilege escalation (`become: true`) to only the tasks that require it.
- Prefer SSH key authentication over passwords; reference key paths via variables.

## Quality
- Run `ansible-lint` and resolve all warnings before committing.
- Validate playbooks with `--syntax-check` and test with `--check --diff` before production runs.
- Write tasks so that `--check` mode produces meaningful output without side effects.
