# dd

## Complete wiping of a USB drive

* Suppose we have a Kali live instance (with persistence) on our USB drive that we wish to completely wipe

```bash
# view the block devices
$ lsblk
...
sda           8:0    1  57.3G  0 disk 
├─sda1        8:1    1   4.3G  0 part /media/user/Kali Live
├─sda2        8:2    1     1M  0 part /media/user/xxxx-xxxx
└─sda3        8:3    1    53G  0 part /media/user/persistence
...

# unmount the partitions
$ sudo umount /dev/sda1 /dev/sda2 /dev/sda3

# erase filesystem signatures: prevents any form of data corruptions, and other related issues
$ sudo wipefs -a /dev/sda

# wipe the data in the device
$ sudo dd if=/dev/zero of=/dev/sda bs=4M status=progress
```

a. **wipefs**

* `-a`, `-all`: erase all available signatures

b. **dd**

* `if=FILE`: read from FILE instead of stdin
  * `if=/dev/zero` simply reads from `/dev/zero` (produces as many null characters (**0x00**) as needed)
* `of`: write to FILE instead of stdout
  * `of=/dev/sda` simply writes to the specified `/dev/sda` block device
* `bs=BYTES`: read and write up to BYTES at a time&#x20;



