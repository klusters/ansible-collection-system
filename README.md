# Ansible Collection - klusters.system
[Inspired by ericsysmin.system](https://galaxy.ansible.com/ericsysmin/system)

Ansible collection that holds roles, that can be used to configure common Linux system. 

## Roles

| Role      | Build Status                                                                                                                                                                                                                                                        | Documentation                                                                                          |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
|  etc_hosts   | ![klusters.system.etc_hosts](https://github.com/klusters/ansible-collection-system/workflows/klusters.system.etc_hosts/badge.svg)          | [Documentation](https://github.com/klusters/ansible-collection-system/tree/master/roles/etc_hosts)    |
|  filesystems   | ![klusters.system.filesystems](https://github.com/klusters/ansible-collection-system/workflows/klusters.system.filesystems/badge.svg)      | [Documentation](https://github.com/klusters/ansible-collection-system/tree/master/roles/filesystems)    |
|  entropy   | ![klusters.system.entropy](https://github.com/klusters/ansible-collection-system/workflows/klusters.system.entropy/badge.svg)      | [Documentation](https://github.com/klusters/ansible-collection-system/tree/master/roles/entropy)    |

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

To be able to test locally:
- install docker 
- install [nektos/act](https://github.com/nektos/act)
- download the huge docker image (18GB) : [nektos/act-environments-ubuntu:18.04](https://hub.docker.com/r/nektos/act-environments-ubuntu/tags)

For example, on MacOS:
```bash
brew cask install docker

brew install act

open /Applications/Docker.app
docker pull nektos/act-environments-ubuntu:18.04
```

Each workflow pertains to a single role, and can be launched locally using the following command:

```bash
act -W .github/workflows/<WORKFLOW_FILE_TO_RUN> \
-P ubuntu-latest=nektos/act-environments-ubuntu:18.04
```

For Google Cloud based workflows : 

```bash
export GCLOUD_PROJECT=<YOUR_GCP_PROJECT_ID>
export GCLOUD_KEYFILE_JSON=$(cat <YOUR_GCP_SERVICE_ACCOUNT_CREDENTIALS_FILE>)

act -s GCLOUD_PROJECT -s GCLOUD_KEYFILE_JSON \
-W .github/workflows/<WORKFLOW_FILE_TO_RUN> \
-P ubuntu-latest=nektos/act-environments-ubuntu:18.04
```
