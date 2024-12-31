---
description: >-
  The mount and umount commands are used to attach (mount) or detach (unmount)
  filesystems to/from the system's directory tree, respectively.
---

# mount/umount

## mount command

The `mount` command can be used to attach a filesystem (such as from a storage device, like a hard drive or USB) to a specific directory on the system's directory tree. This allows the attached filesystem to be accessible from the mount point.&#x20;

**Basic command:**

```bash
$ mount <storage_device> <mount_point> 
```

`<storage_device>`: The storage device or partition to mount (eg. _**/dev/sda1**_, _**/dev/sdb1,**_ etc.)

`<mount_point>`: The directory to mount the filesystem defined by the `<storage_device>` value, to allow it be accessible from (eg. _**/mnt**_, _**/media**_, etc.)

### Example

To mount the device _**/dev/sda1**_ to the _**/mnt/test-mount**_ directory.&#x20;

```bash
$ mount /dev/sda1 /mnt/test-mount
```

This allows the contents of the filesystem on _**/dev/sda1**_ to be accessible from _**/mnt/test-mount.**_ The `chroot` command can be used to change the root directory to _**/mnt/test-mount**_, to be able to work directly from there. ([https://jarrettgxz-sec.gitbook.io/linux/filesystem-and-directories/chroot](https://jarrettgxz-sec.gitbook.io/linux/filesystem-and-directories/chroot))



## umount command

The `umount` command can be used to detach a filesystem. It ensures that the filesystem is properly unmounted before it can be physically removed or shut down.

**Basic command:**

```bash
$ umount <storage_device or mount_point> 
```

`<storage_device or mount_point>`:  Either the storage device that was mounted, or mount point. (eg.   _**/dev/sda1**_, _**/dev/sdb1**_, _**/mnt**_, _**/media**_, etc.)

### Example

To unmount the device _**/dev/sda1**_ (_**/mnt/test-mount**_ directory).&#x20;

```bash
$ umount /dev/sda1 
# OR
$ umount /mnt/test-mount
```

This command unmounts the filesystem, making it no longer accessible from the mount point location.
