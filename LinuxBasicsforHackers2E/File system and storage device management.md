- **[[Mounting]]** : attaching drives or disks to the filesystem to make them accessible to the operating system.
- Newer Serial ATA ([[SATA]]) interface drives and Small Computer System Interface ([[SCSI]]) hard drives are represented as [[sda]]
	- sd==a== ($major\ number$) : First SATA hard drive
	- sdb : Second SATA hard drive
	- sdc : Third SATA hard drive 
	- etc ...
- Some drives can be split into ==partitions== in order to manage and separate information.
	- sda1 ($minor\ number$) : first SATA partition 
	- sda2 : second SATA partition
- `sudo fdisk -l` : lists all the partitions of all the drives.
- file systems used by each os family
	- linux : ext4 ,ext3 ,ext2
	- windows : NTFS (FAT is old)
	- macOS : APFS
___
### Character and Block Devices
- ls [[/dev]] --> ==c==rw------- 1 root root 10, 175 May 16 12:44 agpgart : represent the two ways that devices transfer data in and out.
- c ($character$) : External devices that interact with the system by sending and receiving data character by character (such as mice and keyboard)
- b ($block$) : They communicate in blocks of data (multiple bytes at a time),(hard dirve ,DVD...)
- `lsblk`: lists some basic information about each block device listed in /dev
- `lsusb`: want to know whether a USB device is mounted to our system.
___
### Mounting and Unmounting
- devices such as external USB devices and flash drives can be manually mounted at **/mnt,** but when automatically mounted, the **/media** directory is used (though technically any directory can be used).
- `sudo mount /dev/sda1 /mnt` : mount a drive on the filesystem(The mount point for the device should be an empty directory)
- The filesystems on a system that are mounted at **boot-time** are kept in a file at **/etc/fstab** (short for filesystem table), which is read by the system at every bootup.
- `sudo umount /dev/sdb1`
- `df` :provide us with basic information on any hard disks or mounted devices
- `fsck` : **checks** the filesystem for errors and **repairs** the damage, if possible, or else puts the **bad area** into a **bad blocks** table to mark it as bad.(I can add the -p option to have fsck automatically repair any problems with the device)
- 