# klusters.system.filesystems

This role formats and mount block devices according to the *dev_mapping* list

This role has been created to prepare storage on freshly installed machines. We use this role prior to Elasticsearch, Kafka, and Hadoop clusters deployment

## Requirements

# This role is not tested yet !

## Examples

```yaml
- hosts: all
  gather_facts: false
  strategy: free

  roles:
    - role: klusters.system.filesystems
      vars: 
        default_fs_type: 'ext4'
        dev_mapping:
          - dev_name: /dev/sdb
            mount_path: /var/log

          - dev_name: /dev/sdc
            mount_path: /home
            fs_type: xfs

```

## ToDo

  - [ ] Feat. : Add mkfs options
  - [ ] Feat. : Add LVM support (PV/VG/LV)
  - [ ] Feat. : Write fs' UUID to /etc/fstab to handle disordered block devices connection
  - [ ] Feat. : Use var to handle block device naming rules (xvd/sd/vd)
  - [x] Feat. : Add documentation
  - [ ] Tests : Add GCP tests (via Molecule + Vagrant ?)
  - [ ] Tests : Add AWS tests (via Molecule + Vagrant ?)