# klusters.system.filesystems

This role formats and mount block devices according to the *dev_mapping* list

This role has been created to prepare storage on freshly installed machines. We use this role prior to Elasticsearch, Kafka, and Hadoop clusters deployment

## Requirements

This role is tested against :
  - CentOS 7 & 8
  - Ubuntu 18.04 & 20.04

This role will only configure block devices existing on the remote host, i.e. it will not fail if a block device in `dev_mapping` is not found on the host, it will just skip it. This helps to configure an entire cluster with different disks configuration (e.g. Elasticsearch Cluster with 2 Masters, 2 Coordinators, and 6 Datanodes : Masters & Coordinators will have /data/01 only and Datanodes will have /data/01..12 but both will have system FS : /var/log, etc...)

## Role Variables

| Variable                 | Required | Default                                                                  | Comments                                        |
| ------------------------ | -------- | ------------------------------------------------------------------------ | ----------------------------------------------- |
| `default_fs_type`       | No       | `xfs`                                                                | Set fs type if not defined in dev_mapping         |
| `dev_mapping`   | No       | `see defaults/main.yml`                                                                | List filesystems to create, mount path, fstype, mkfs & mount options |
| `volume_groups` | No       | `vg.data`                                                                    | List of Volume groups to create                   |
| `logical_volumes`   | No       | `see defaults/main.yml` | List of LV to create                   |


## Examples

```yaml
# Simple example with :
# - /dev/sdb formatted in ext4 and mounted in /var/log
# - /dev/sdc formatted in xfs and mounted in /opt

- hosts: all
  strategy: free

  roles:
    - role: klusters.system.filesystems
      vars: 
        default_fs_type: 'ext4'
        dev_mapping:
          - dev_name: /dev/sdb
            mount_path: /var/log

          - dev_name: /dev/sdc
            mount_path: /opt
            fs_type: xfs
```

```yaml
# Example with pre-existing vg.data on the host (e.g. part of your company os image):
# - lv.home.user1 formatted in xfs and mounted in /home/user1
# - lv.home.user2 formatted in xfs and mounted in /home/user2

- hosts: all
  strategy: free

  roles:
    - role: klusters.system.filesystems
      vars: 
        dev_mapping: []
        volumes_groups: []
        logical_volumes:
          - name: lv.home.user1
            vg: vg.data
            size: 500M
            mount_path: /home/user1

          - name: lv.home.user2
            vg: vg.data
            size: 400M
            mount_path: /home/user2
```

## ToDo

  - [x] Feat. : Add mkfs & mount options
  - [x] Feat. : Add LVM support (PV/VG/LV)
  - [ ] Feat. : Write fs' UUID to /etc/fstab to handle disordered block devices connection
  - [x] Feat. : Add documentation
  - [x] Feat. : Add vars to documentation
  - [x] Tests : Add GCP tests
  - [ ] Tests : Add AWS tests