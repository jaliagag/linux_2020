
The swap partition is a separate partition that moves items from computer memory to its hard drive. You can check for the swap partition and its space in Linux by entering the following command:

`swapon -s`

Note: The swap partition size depends on the amount of RAM in the system.

You can also list all the partitions on the hard disk and their mount points by entering the following command:

`mount`

The hard disk on a system must be partitioned before you can use it. Information about these partitions is recorded in the MBR (Master Boot Record) and GPT (GUID Partition Table) on the drive. In this exercise, you will understand how to create partitions and filesystems on a disk.

Each hard disk contains one MBR partition. It is the first sector of the disk and is not large enough to hold more than four partitions. These partitions can be:

- Primary
- Extended
- Logical

There can be a variation on the number of primary and extended partitions that you can define. For example, you can have three primary partitions and one extended partition. Else, you can have one primary and one extended split into three logical partitions and many more.

You can display the partition table using the parted command that shows you the boot partition and its type.

To display the partition table, type the following command:

`sudo parted /dev/sda u s p`

- u - An abbreviation for Unit command.
- s - Refers to the unit Sector, this can be interchanged with the following:  B, KiB, MiB, GiB, TiB, kB, MB, GB, TB, %, cyl, chs, compact.
- p - An abbreviation for Print command.

You can also list the partitions using the fdisk.

To list the partitions, enter the following command:

`sudo fdisk -l /dev/sda`

You can also list the partitions using the fdisk.

To list the partitions, enter the following command:

`sudo fdisk -l /dev/sdb`

Using the fdisk command, you can also create or remove partitions from a device, such as /dev/sdb.

`sudo fdisk /dev/sdb`

This command displays the list of options to work with partitions on the /dev/sdb device.

To see the list of options, type the following:

`m`

To display the existing partition table, type the following:

`p`

Currently, the disk has two partitions and no free space. You will first delete a partition and then create a new partition. To delete a partition, type the following:

`d`

When prompted for the partition number, type the following number:

`2`

You are prompted with the message that the partition has been deleted. To display the existing partition table, type the following:

p

Press Enter.

Notice that only one partition is now left.

You will now create a new partition. Type the following:

n
Press Enter. You will be prompted to specify whether the partition needs to be a primary or an extended partition.

To create a primary partition, type the following:

p
Press Enter.

You will now be prompted to enter the partition number.

To enter the partition number, type the following number:

2
Press Enter. You will now be prompted to enter the first sector.

You can accept the default value as the first sector. To do this, press Enter.

Note: You can enter any number. However, it is suggested that you should enter the first sector of the disk to start with. Else, you waste this space.

You can accept the default value as the last sector. However, for this task, type the following:

35000000
Press Enter. You will then be prompted to remove the signature.

You are prompted that the disk contains the ext4 signature. Type the following:

Y

GPT is the latest standard for defining the partitions on a hard disk. GPT uses globally unique identifiers (GUID) to define the partition, and you can create theoretically unlimited partitions on the hard disk. In this task, you will create and access a GPT table on the /dev/sdb device.

To manage GPT tables, perform the following tasks:

Step 1
Clear the screen by entering the following command:

clear
You can use the gdisk command to create a GUID Partition Table (GPT) and a partition. To create a GUID Partition Table, type the following command:

sudo gdisk /dev/sdb
Press Enter. You will need to enter an option to proceed.

Figure 1.19 Screenshot of PLABLINUX02
Figure 1.19 Screenshot of PLABLINUX02: Creating a GUID Partition Table.
Step 2
To create a new partition, type the following:

n
Press Enter.

You will now be prompted to enter the partition number.

Figure 1.20 Screenshot of PLABLINUX02
Figure 1.20 Screenshot of PLABLINUX02: Creating a new partition.
Step 3
For this task, type the partition number as:

3
Press Enter.

You will now be asked for the first sector. Press Enter to accept the default.

Figure 1.21 Screenshot of PLABLINUX02
Figure 1.21 Screenshot of PLABLINUX02: Setting the partition number.
Step 4
You will now be prompted for the last sector. Press Enter to accept the default.

Figure 1.22 Screenshot of PLABLINUX02
Figure 1.22 Screenshot of PLABLINUX02: Accepting the default last sector of the partition.
Step 5
To define GUID, type the following:

8300
Press Enter.

Note: The command indicates that pressing enter with nothing entered will accept the suggested default of 8300, this results in a Linux filesystem.
Figure 1.23 Screenshot of PLABLINUX02
Figure 1.23 Screenshot of PLABLINUX02: Defining the GUID for the partition.
Step 6
On the next prompt, to print the partitions, type the following:

p
Press Enter.

Notice that details of both the partitions created till now are listed.

Figure 1.24 Screenshot of PLABLINUX02
Figure 1.24 Screenshot of PLABLINUX02: Printing the partition information.
Step 7
Type the following to write the partitions:

w
Press Enter.

You will be prompted to confirm your choice.

Figure 1.25 Screenshot of PLABLINUX02
Figure 1.25 Screenshot of PLABLINUX02: Writing the partition.
Step 8
To confirm your choice, type the following:

Y
Press Enter.

Note: A warning is shown that the kernel is still using the old partition table and that the new table will be used at the next reboot. You can complete the reboot or continue to the next step.
Figure 1.26 Screenshot of PLABLINUX02
Figure 1.26 Screenshot of PLABLINUX02: Confirming the writing of the partition information.
Step 9
Clear the screen by entering the following command:

clear
To verify that the new partition table is now created and there is a new partition on /dev/sdb, type the following command:

sudo fdisk -l
Press Enter.

Figure 1.27 Screenshot of PLABLINUX02
Figure 1.27 Screenshot of PLABLINUX02: Verifying the new partition table.
Step 10
Clear the screen by entering the following command:

clear
Using the mkswap command, you can also create the swap space on a partition. However, before you proceed with creating the swap space, you need to unmount the partition. Type the following command:

sudo umount /dev/sdb2
Press Enter.

Figure 1.28 Screenshot of PLABLINUX02
Figure 1.28 Screenshot of PLABLINUX02: Unmounting the partition.
Step 11
To create swap space on the sdb2 partition, type the following command:

sudo mkswap /dev/sdb2
Press Enter.

Figure 1.29 Screenshot of PLABLINUX02
Figure 1.29 Screenshot of PLABLINUX02: Creating the swap space on the /dev/sdb2 partition.
Task 3 - Create Various Filesystems
You can create different types of filesystems, such as ext2, ext3, and ext4, with the mkfs command. In this task, you will create an ext3 filesystem on the sdb1 partition created in the earlier task.

To create a filesystem, perform the following steps:

Step 1
Clear the screen by entering the following command:

clear
In the previous task, you noticed that /dev/sdb1 had been created.

To create a filesystem on this partition, type the following command:

sudo mkfs -t ext3 /dev/sdb2
Press Enter. Note that ext3 is a type of filesystem.

Figure 1.30 Screenshot of PLABLINUX02
Figure 1.30 Screenshot of PLABLINUX02: Creating a filesystem on this partition.
Step 2
When prompted for confirmation, type the following:

y
Press Enter.

Note: You can similarly create the ext2 and ext4 type of filesystems.
Figure 1.31 Screenshot of PLABLINUX02
Figure 1.31 Screenshot of PLABLINUX02: Confirming the partition type.
Step 3
To verify the type of partition being used, type the following command:

sudo lsblk -f
Press Enter.

Notice that sdb2 is of the ext3 file system.

Till this point, you have created a partition table in the memory. To save the table, you write the table to the memory of the device. To write the partition table, type the following:

w
