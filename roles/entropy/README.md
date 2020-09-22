Ansible Role: entropy
==================

[Adapted from giovtorres/ansible-role-rngd](https://github.com/giovtorres/ansible-role-rngd)

Install rngd tools and select the random generator device to use

## Requirements

This role is tested against :
  - CentOS 7 & 8
  - Ubuntu 18.04 & 20.04

## Role Variables

| Variable                 | Required | Default                                                                  | Comments                                        |
| ------------------------ | -------- | ------------------------------------------------------------------------ | ----------------------------------------------- |
| `rngd_device`       | No       | `/dev/urandom`                                                                | Name of the device to use (rngd -v)         |

## Examples

```yaml
- hosts: all
  gather_facts: false
  strategy: free

  roles:
    - role: klusters.system.entropy
```