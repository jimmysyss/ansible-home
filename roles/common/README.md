# common role

Applies baseline host configuration shared across all targets.

## Role Variables
- `common_install_enabled`: Enables package installation/bootstrap tasks.
- `common_maintenance_enabled`: Enables maintenance workflow (update/upgrade/reboot checks).
- `common_docker_update_enabled`: Enables docker update workflow in this role.
- `common_docker_update_force`: Forces image pull and recreation even when image digest is unchanged.
- `common_docker_update_label`: Label filter used to discover containers for update (default: `autoupdate=true`).

## Docker Update Workflow

The docker update workflow is implemented in `tasks/docker_update.yml` and is intentionally manual-triggered.

- It is tagged with `docker_update`, so it runs when explicitly requested.
- It discovers managed containers by label using `common_docker_update_label`.
- It pulls newer images and updates containers only when image changed (or when `common_docker_update_force` is enabled).
- For Docker Compose-managed containers, it runs `docker compose up -d <service>` to preserve compose runtime configuration.
- For non-compose containers, it recreates with `community.docker.docker_container` and ensures started state.

### Example Host Variables

```yaml
common_docker_update_enabled: true
common_docker_update_force: false
common_docker_update_label: "autoupdate=true"
```

### Manual Execution

```bash
ansible-playbook -i inventory/production site.yml --limit server8.jimmysyss.com --tags docker_update --check --diff -K
ansible-playbook -i inventory/production site.yml --limit server8.jimmysyss.com --tags docker_update -K
```
