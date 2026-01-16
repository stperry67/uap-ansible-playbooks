# Ansible Playbooks for UAP

This repository contains Ansible playbooks used by the Unified Automation Platform (UAP).

## Directory Structure

- `playbooks/` - All playbooks organized by category
  - `infrastructure/` - System management playbooks
  - `security/` - Security and compliance playbooks
  - `applications/` - Application deployment playbooks
  - `monitoring/` - Monitoring and health check playbooks
- `roles/` - Reusable Ansible roles
- `inventory/` - Inventory files (not used by UAP, for reference only)
- `group_vars/` - Group variables (not used by UAP, for reference only)
- `templates/` - Jinja2 templates used by playbooks

## Usage with UAP

Playbooks are referenced by path relative to repository root:
```json
{
  "operation": "run_playbook",
  "playbooks_repo_url": "https://github.com/your-org/ansible-playbooks.git",
  "playbooks_repo_file": "playbooks/infrastructure/system-info.yml",
  "target_hosts": ["server01.example.com"]
}
```

## Playbook Standards

### File Naming
- Use kebab-case: `system-info.yml`, `patch-servers.yml`
- Be descriptive but concise
- Extension must be `.yml` or `.yaml`

### Playbook Structure
All playbooks should include:
```yaml
---
- name: Clear description of what this playbook does
  hosts: all
  gather_facts: yes  # or no if not needed
  
  tasks:
    - name: Each task has a clear name
      # ... task definition
```

### Variables
- Use `extra_vars` for runtime configuration
- Document required variables in playbook comments
- Provide sensible defaults where possible

### Testing
Before committing:
1. Validate syntax: `ansible-playbook --syntax-check playbook.yml`
2. Run in check mode: `ansible-playbook --check playbook.yml`
3. Test on development systems

## Version Control

- `main` branch - Production-ready playbooks
- `develop` branch - Development/testing
- Feature branches - `feature/new-playbook-name`

Tag releases: `v1.0.0`, `v1.1.0`