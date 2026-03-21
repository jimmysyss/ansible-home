---
applyTo: "**/*.yml,**/*.yaml"
description: "Performance optimisation standards for ansible-home"
---

# Performance Standards

Apply the repository-wide guidance from `../copilot-instructions.md` to all performance considerations.

## Parallelism & Forks
- Set `forks` in `ansible.cfg` to match the number of hosts you manage concurrently — the default of 5 is often too low for server fleets.
- Use `serial` at the play level to control rolling deployments on the gateway and hosting roles, preventing entire-fleet outages.

## Task Efficiency
- Avoid running the same package installation or file operation in multiple roles — centralise common setup in the `common` role.
- Use `loop` (not `with_items`) for installing multiple packages in a single task to reduce module call round-trips.
- Prefer `ansible.builtin.apt` with `update_cache: true` only when necessary, or use a dedicated cache-refresh task guarded by a `when` condition.

## Fact Gathering
- Disable fact gathering (`gather_facts: false`) on plays that do not need host facts to reduce overhead on large runs.
- Use `ansible.builtin.setup` with `filter` when only a subset of facts is required.

## Handler Batching
- Use handlers and `notify` rather than restarting services inline — handlers run once at the end of a play, even if notified multiple times.
- Group service restarts into a single handler flush with `meta: flush_handlers` only when ordering is critical.

## Caching
- Enable fact caching (`fact_caching = jsonfile` or `redis`) in `ansible.cfg` for large inventories to avoid redundant SSH connections.
- Use `delegate_to` and `run_once` for tasks that only need to execute on a single host (e.g., database schema migrations).

## Template Rendering
- Keep Jinja2 templates focused and avoid complex logic inside templates — move conditional logic into variables or tasks.
- Use `ansible.builtin.template` validation (the `validate` parameter) for critical configuration files to catch errors before overwriting.
