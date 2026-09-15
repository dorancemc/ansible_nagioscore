# Nagios Core

Install and configure Nagios Core with Apache, optional NRDP and PNP4Nagios.

This role installs the engine only. Monitoring objects (hosts, services, contacts, groups, templates) belong to [`ansible_nagiosconfig`](https://github.com/dorancemc/ansible_nagiosconfig). A shipped `bootstrap.cfg` provides minimal self-contained objects so a fresh install passes `nagios -v` and starts cleanly.

## Requirements

- Ansible 2.20 or newer
- Enterprise Linux 9 (AlmaLinux, Rocky, RHEL, Oracle Linux), Debian 13, or Ubuntu 24.04
- Root privileges on target hosts

Amazon Linux 2023 is not supported.

## Example Playbook

```ini
[nagios]
nagios.example.com ansible_host=192.168.243.220
```

```yaml
- hosts: nagios
  become: true
  roles:
    - role: dorancemc.ansible_nagioscore
```

```bash
ansible-playbook --limit nagios playbook.yml --tags nagioscore
```

Tags: `nagioscore`, `nagioscore-install`, `nagioscore-apache-config`, `nagioscore-nrdp`, `nagioscore-nrdp-config`, `nagioscore-pnp4nagios`.

## Variables

Defaults live in `defaults/`. Key items:

- `nagioscore_htpasswd_users` — dict of `user: {password, state}` for the Apache `AuthUserFile`.
- Vault credentials: `vault_nagiosadmin_password`, `vault_rouser_password`, `vault_nrdp_mysecrettoken`, `vault_nrdp_myothertoken`.
