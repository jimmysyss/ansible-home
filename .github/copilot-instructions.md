# ansible-home — Copilot Instructions

## Project Overview
Personal home-lab Ansible project that automates provisioning and configuration of a mixed fleet: Ubuntu servers (`jimmysyss.com`), a GUI desktop, a Raspberry Pi, Proxmox hypervisor, OpenMediaVault NAS, and gateway/router hosts. The goal is idempotent, declarative infrastructure-as-code for a self-hosted home environment.

## Tech Stack
- **Automation**: Ansible (latest stable)
- **Target OS**: Ubuntu (servers & desktop), Debian / Raspberry Pi OS, Proxmox VE, OpenMediaVault
- **Collections**: `community.mysql`, `community.postgresql`
- **Package manager**: `apt` (all targets are Debian-family)
- **Inventory**: INI-format, `inventory/production` and `inventory/staging`
- **Variable layering**: `group_vars/` → `host_vars/`

## Repository Layout
```
ansible-home/
├── ansible.cfg
├── requirements.yml          # Galaxy collections & roles
├── inventory/
│   ├── production            # Real hosts
│   └── staging
├── group_vars/               # Variables per group (all.yml, server.yml, desktop.yml, …)
├── host_vars/                # Per-host overrides
├── roles/
│   ├── common/               # Applied to every host
│   ├── desktop/              # GUI desktop setup (with_gui: true)
│   ├── gateway/              # Routing / firewall
│   ├── hosting/              # Web hosting stack
│   └── nginx/                # nginx configuration
├── filter_plugins/           # Custom Jinja2 filters
├── library/                  # Custom modules
└── module_utils/             # Shared module utilities
```

## Conventions

### Naming
- Role names: `snake_case`, descriptive (e.g., `nginx`, `common`, `desktop`)
- Task names: Human-readable sentences, Title Case (e.g., `Install required packages`)
- Variables: `snake_case`, prefixed with role name for role-specific vars (e.g., `nginx_port`)
- Tags: `snake_case`, consistent across roles (e.g., `packages`, `config`, `service`)

### Structure
- Every role follows the standard Ansible layout: `tasks/`, `handlers/`, `defaults/`, `vars/`, `files/`, `templates/`, `meta/`
- `tasks/main.yml` is the entry point; break large task lists into `tasks/subtask.yml` files included via `include_tasks`
- Use `defaults/main.yml` for all user-overridable variables with sensible defaults
- Use `vars/main.yml` only for constants that should not be overridden
- Templates use `.j2` extension

### Style
- Always use YAML syntax (not `key=value` inline style) for task arguments
- Prefer `ansible.builtin.*` fully-qualified collection names (FQCN) for all built-in modules
- Use `block:` / `rescue:` / `always:` for error handling
- Handlers are `snake_case` verbs (e.g., `restart nginx`, `reload systemd`)

## Workflow
- Branch naming: `feature/<description>`, `fix/<description>`, `chore/<description>`
- Commit style: conventional commits (`feat:`, `fix:`, `chore:`, `docs:`)
- Test playbooks against `inventory/staging` before `inventory/production`
- Run `ansible-lint` before committing

## Instruction Files
Detailed standards live in `.github/instructions/`:
- Ansible guidelines: `.github/instructions/ansible.instructions.md`
- Testing: `.github/instructions/testing.instructions.md`
- Security: `.github/instructions/security.instructions.md`
- Documentation: `.github/instructions/documentation.instructions.md`
- Performance: `.github/instructions/performance.instructions.md`
- Code review: `.github/instructions/code-review.instructions.md`
