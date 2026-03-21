---
applyTo: "**/*.yml,**/*.yaml,**/*.j2,**/*.md"
description: "Code review standards for ansible-home"
---

# Code Review Standards

Apply the repository-wide guidance from `../copilot-instructions.md` to all code reviews.

## Review Checklist

### Correctness
- All tasks have meaningful `name` fields in Title Case.
- Modules use fully-qualified collection names (FQCN).
- Task arguments use YAML dict syntax — no inline `key=value` style.
- Conditional logic (`when:`) is clear and uses correct variable types.
- Templates render the intended values and handle missing variables gracefully with defaults.

### Idempotency
- Re-running the role/playbook produces zero `changed` tasks after the first successful run.
- File/template tasks do not unconditionally overwrite content — verify `checksum` or `mode` guards are in place where necessary.
- `command`/`shell` tasks have an appropriate `creates`, `removes`, or `changed_when` guard.

### Security
- No plaintext secrets or credentials are present in any file.
- `become: true` is scoped to individual tasks, not entire plays.
- New firewall or network rules are explicitly commented with their purpose.

### Structure & Conventions
- New variables have defaults defined in `defaults/main.yml`.
- Handlers follow the `snake_case` verb convention and are named consistently.
- Include/import choices (`include_tasks` vs `import_tasks`) are intentional and documented when non-obvious.

### Testing
- The change has been tested against `inventory/staging` before being applied to production.
- Idempotency has been verified with a second run.
- `ansible-lint` and `--syntax-check` pass cleanly.

## Review Etiquette
- Raise questions as constructive suggestions, not mandates — this is a personal project.
- Flag potential breakages on other hosts when a change targets a shared group var or common role.
- Approve only after staging validation is confirmed.
