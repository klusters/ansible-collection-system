# Ansible Collection - klusters.system
[Inspired by ericsysmin.system](https://galaxy.ansible.com/ericsysmin/system)

Ansible collection that holds roles, that can be used to configure common system services. 

## Roles

| Role      | Build Status                                                                                                                                                                                                                                                        | Documentation                                                                                          |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
|  etc_hosts   | ![klusters.system.etc_hosts](https://github.com/klusters/system/workflows/Ansible%20Tests/badge.svg)          | [Documentation](https://github.com/klusters/system/tree/docs/roles/etc_hosts)    |
|  filesystems   | Local tests with vbox      | [Documentation](https://github.com/klusters/system/tree/docs/roles/filesystems)    |

## Usage

You can find specific to each role within the "Documentation" link for each role. However, most should be in this format:

Install this ansible collection :
```bash
ansible-galaxy collection install klusters.system
```

Write a playbook file *playbook_name.yml* :

```yaml
---
- hosts: localhost

  tasks:
    - include_role:
        name: klusters.system.<role_name>
```

Run *playbook_name.yml* :
```bash
ansible-playbook playbook_name.yml
```

## Testing

Testing is done through GitHub Actions, and can be tested locally as well.

Each workflow pertains to a single role, and can be launched locally using the following command:

```bash
MOLECULE_COMMAND={{ matrix.molecule_distro.command }} \
MOLECULE_DISTRO={{ matrix.molecule_distro.distro }} \
molecule test -s {{ matrix.collection_role }}
```

To decide on the `MOLECULE_COMMAND` value please refer to the `.github/workflow/{{ collection_role }}.yml` file as it will have the value for proper systemd services.