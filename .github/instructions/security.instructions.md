---
applyTo: "**/*.yml,**/*.yaml,**/*.j2"
description: "Security standards for ansible-home"
---

# Security Standards

Apply the repository-wide guidance from `../copilot-instructions.md` to all security-related decisions.

## Secrets Management
- Never commit plaintext passwords, API keys, tokens, or private keys to the repository.
- Use `ansible-vault` to encrypt all sensitive variables; store vault-encrypted files in `group_vars/` or `host_vars/` alongside plain variables.
- Reference secrets through variables, never inline in task arguments or templates.
- Rotate vault passwords periodically and store the vault password securely outside the repository.

## Privilege Escalation
- Apply `become: true` at the task level only, not at the play level — this limits the blast radius of escalated privileges.
- Always specify `become_user` explicitly when escalating to a user other than root.
- Avoid passwordless sudo in production; prefer SSH key authentication and per-task escalation.

## SSH & Authentication
- Prefer SSH key-based authentication for all managed hosts; reference key paths via variables.
- Disable root SSH login on managed servers where possible; use a dedicated `ansible_user` with sudo access.
- Set `host_key_checking = true` in `ansible.cfg` for production — only disable for ephemeral staging environments.

## Firewall & Network
- gateway-role changes must follow a least-privilege approach: deny by default, allow explicitly.
- Document the purpose of every firewall rule in a task comment or `name` field.
- Avoid opening ports beyond what the service requires.

## Package & Dependency Security
- Pin critical package versions where stability and security predictability matter.
- Regularly review `requirements.yml` for outdated or unmaintained Galaxy roles and collections.
- Prefer official `ansible.builtin.*` modules over external roles when functionality overlaps.

## Audit & Logging
- Ensure that logging and auditing services (e.g., `auditd`, `syslog`) are configured and running on server hosts.
- Do not suppress Ansible output (`no_log: true`) except for tasks that explicitly handle secrets — and document the reason.
