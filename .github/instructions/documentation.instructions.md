---
applyTo: "**/*.yml,**/*.yaml,**/*.md,**/*.j2"
description: "Documentation standards for ansible-home"
---

# Documentation Standards

Apply the repository-wide guidance from `../copilot-instructions.md` to all documentation.

## Inline Documentation
- Every task `name` should read as a plain-English sentence describing the desired outcome, not the action (e.g., `Ensure nginx is running` not `Start nginx`).
- Add inline comments (`# ...`) above non-obvious tasks to explain *why* the task exists, not just what it does.
- Document non-default variable values in `defaults/main.yml` with a brief comment explaining acceptable values or impact.

## Role Documentation
- Every role should have a `README.md` in the role root that covers: purpose, requirements, role variables (with defaults and descriptions), dependencies, and a usage example.
- List role dependencies in `meta/main.yml` and keep it updated.

## Variable Documentation
- Group variable files (`group_vars/`, `host_vars/`) should include comments explaining what the group is and which roles consume the variables defined there.
- Document any variable that has a non-obvious default value or that influences conditional logic.

## Playbook Documentation
- Top-level playbooks should include a header comment block describing: purpose, which inventory groups it targets, and any prerequisites.
- Reference relevant instruction files or external docs where useful.

## Changelog & Commit Messages
- Follow conventional commits: `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`, `test:`.
- Commit messages should describe *what changed and why*, not just *what was done*.
- Keep `readme.md` updated with any new setup steps or changed workflows.
