---
name: generate-docs
description: Generate documentation for Ansible roles and playbooks
---

# Generate Docs

Create or update documentation for Ansible roles and playbooks, following the standards in `.github/instructions/documentation.instructions.md`.

## What To Do

### Role README
Generate a `README.md` for the role that includes:
- **Purpose** — one-paragraph description of what the role does and which host groups use it.
- **Requirements** — minimum Ansible version, OS family, and any prerequisite roles/collections.
- **Role Variables** — a Markdown table with columns: Variable | Default | Description.
- **Dependencies** — list any roles in `meta/main.yml`.
- **Example Playbook** — a minimal playbook snippet showing how to use the role.

### Inline Comments
- Add `# ...` comments above non-obvious tasks explaining *why*, not just *what*.
- Add comments to `defaults/main.yml` entries that have non-obvious acceptable values.

### Playbook Headers
Add a YAML comment block at the top of playbooks covering:
- Purpose
- Target inventory groups
- Key variables that affect behaviour
- Prerequisites or order dependencies

Keep all documentation concise and accurate — prefer short, precise sentences over verbose prose.
