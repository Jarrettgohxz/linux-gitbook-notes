---
description: >-
  The lsblk (list block devices) command in Linux is used to list information
  about all available or specified block devices.
---

# lsblk

Block devices are storage devices that can be used to store data in blocks (e.g., hard drives, solid-state drives, USB drives, and partitions). This command provides detailed information about these devices, such as their names, sizes, types, and mount points.

The simple `lsblk` command can be used:

```bash
$ lsblk 

NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINTS
sda     ...    1    400G 0  disk
├─sda1  ...    1    300G 0  part /mnt/test-mount                         
└─sda2  ...    1    100G 0  part 

```

This simply displays the all the block devices, along with their partitions and mount points. The output displays the following:

1. _**sda**_ is a disk with 400 GB of storage
2. _**sda**_ has partitions of _**sda1**_ and _**sda2**_
3. _**sda1**_ is mounted at _`/mnt/test-mount`_ refer to the _mount/unmount_ sub-section in this section for more information about mounting filesystems: [https://jarrettgxz-sec.gitbook.io/linux/storage/mount-umount](https://jarrettgxz-sec.gitbook.io/linux/storage/mount-umount))

