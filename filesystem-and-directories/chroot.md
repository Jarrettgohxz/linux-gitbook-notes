---
description: >-
  The chroot command changes the root directory (/) for the current running
  process by creating a secured contained environment known as a "chroot jail".
---

# chroot

**Basic command:**

```bash
$ chroot </path/to/chroot-jail>
```

This command change the root directory to _**/path/to/chroot-jail.**_ Any processes running inside this _"chroot jail"_ will not have access to the actual root filesystem that is outside this _"jail"_.

### Example

Suppose there is a mounted filesystem at the directory _**/mnt/temp-mnt-loc**_ (refer to the documentation for the `mount` command: [https://jarrettgxz-sec.gitbook.io/linux/storage/mount-umount](https://jarrettgxz-sec.gitbook.io/linux/storage/mount-umount))

```bash
$ mount <storage_device> /mnt/temp-mnt-loc
```

The `ls /` command will list the contents of the user system's root directory (`/`).

```bash
$ ls /
... file-at-user-root-dir.txt
...
```

After the `chroot` command have been used to change the root directory to the mounted location, any commands ran will use the directory supplied as the new root directory. Note that the `chroot` command changes the root directory only for the current process and its child process, but doesn't affect other processes on the system or the actual root directory of the system.&#x20;

```bash
$ chroot /mnt/temp-mnt-loc
```

The `ls /` command will list the contents of the new root directory, which is the mounted filesystem (_**/mnt/temp-mnt-loc**_). This is because _**/mnt/temp-mnt-loc**_ is now perceived as the new `/` (root directory). This will have the same output if the command is ran directly with the mounted location as input.

```bash
 $ ls /
... file-at-mounted-dir.txt
... 

$ ls /mnt/temp-mnt/loc
... file-at-mounted-dir.txt
...
```



