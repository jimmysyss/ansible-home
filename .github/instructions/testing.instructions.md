---
applyTo: "**/*.yml,**/*.yaml"
description: "Testing and validation standards for ansible-home"
---

# Testing Standards

Apply the repository-wide guidance from `../copilot-instructions.md` to all testing activities.

## General Principles
- Always validate changes in `inventory/staging` before promoting to `inventory/production`.
- Treat every playbook run as a test — every task should report a meaningful changed/ok/failed status.
- Idempotency is a first-class requirement: running the same role twice must produce zero changes on the second run.

## Syntax and Lint Checks
- Run `ansible-lint` against all modified files before every commit and resolve all warnings.
- Run `ansible-playbook --syntax-check` for every playbook to catch YAML and structural errors early.
- Use `yamllint` to enforce consistent YAML formatting across the repository.

## Dry-Run Testing
- Use `--check --diff` mode to preview changes before applying to any host.
- Review the diff output carefully for unintended changes, especially in templates and file tasks.
- When `--check` mode is insufficient (e.g., for `command`/`shell` tasks), add `check_mode: false` intentionally and comment why.

## Staging Workflow
- Map every production group to an equivalent staging group in `inventory/staging`.
- Run the full affected playbook against staging before touching production.
- Validate the service or configuration is correct on staging hosts before proceeding.

## Idempotency Testing
- After a successful playbook run, immediately rerun the playbook and confirm all tasks report `ok` (zero `changed`).
- Pay special attention to template rendering, file line-edits, and command tasks when verifying idempotency.

## Molecule (aspirational)
- New roles should include a `molecule/` directory with at least a default scenario when time allows.
- Molecule tests should verify the role converges successfully and passes an idempotency check.
