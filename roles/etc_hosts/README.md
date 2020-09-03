# klusters.system.etc_hosts

This role writes ip address (*ansible_default_ipv4.address*) and fqdn (*ansible_fqdn*) from every host in the inventory to /etc/hosts file.

This role has been created because we didn't find any scalable role. Each host will gather network facts from all other hosts. That's how, we ensure that every host will be written in every hosts' /etc/hosts file, even when using '*strategy: free*' and '*gather_facts: false*'

## Requirements

This role is tested against :
  - CentOS 8
  - Ubuntu 18.04 & 20.04

## Examples

```yaml
- hosts: all
  gather_facts: false
  strategy: free

  roles:
    - role: klusters.system.etc_hosts
```

## ToDo

  - [ ] Fix : CentOS 7 tests (Ansible cannot gather network facts from CentOS 7 in Docker container)
  - [ ] Feat. : Add the posibility to choose the ip address & fqdn hostvars used by role's template
  - [x] Feat. : Add documentation
  - [ ] Tests : Add assertions