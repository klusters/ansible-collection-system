Ansible Role: tcp-offload
==================

Configure tcp offload

## Requirements

This role is tested against :
  - CentOS 7 & 8
  - Ubuntu 18.04 & 20.04

## Examples

```yaml
- hosts: all
  strategy: free

  roles:
    - role: klusters.system.tcp-offload
```