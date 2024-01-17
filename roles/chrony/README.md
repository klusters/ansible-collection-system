Ansible Role: chrony
==================

[Adapted from ericsysmin/ansible-collection-system/chrony](https://github.com/ericsysmin/ansible-collection-system)

Install rngd tools and select the random generator device to use

## Requirements

This role is tested against :
  - EL 7 & 8 & 9

## Role Variables

| Variable                 | Required | Default                                                                  | Comments                                        |
| ------------------------ | -------- | ------------------------------------------------------------------------ | ----------------------------------------------- |
| `chrony_service_state`       | No       | `started`                                                                | Chronyd wanted service state         |
| `chrony_config_servers`       | No       | `['0.pool.ntp.org', '1.pool.ntp.org', '2.pool.ntp.org', '3.pool.ntp.org']` | List of NTP servers to use         |
| `chrony_config_logdir`       | No       | `/var/log/chrony` | Log directory         |
| `chrony_service_name`       | No       | `chronyd` | Service name         |
| `chrony_config_location`       | No       | `/etc/chrony.conf` | Configuration file path         |
| `chrony_config_driftfile`       | No       | `/var/lib/chrony/drift` | Drift file path         |
| `chrony_config_keyfile`       | No       | `/etc/chrony.keys` | Keys path         |
| `chrony_config_extra_options`       | No       | `{}` | Any extra options supported by Chrony         |

## Examples

```yaml
- hosts: all
  gather_facts: false
  strategy: free

  roles:
    - role: klusters.system.chrony
```