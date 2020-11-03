# CompTIA Linux+

## Introduction to Linux & the Command Line

- Free software: You can view, modify, copy and distribute software. Social movement, focus on User rights
- Open Source: View modify distribute copy - development methodologoy, focus on collaboration; sharing soure code to receive feedback - you can't distribute it freely? as long as you don't make money

Linux is a kernel - software that allows software to talk to hardware. The kernel runs on top of the Hardware.

GNU: Focus on _free_. The entire software is free.

People take GNU software + linux kernel -- > linux distribution. 

### Shell prompt

- $ regular user
- # root

Shell --> bash, zsh, dash

| command | option | args |
| ------- | ------ |---- |
| ls | -la | /bin/sh |

Super User: make modifications to the system - or to make changes in behalf of the another user.

If there's [] --> optional; if there is no [], that's mandatory.

Using a hyphen when logging in, we are _creating a session_ for that user. You are _fully_ that user; if you don't use the hyphen, you are modifying your session, instead of creating a _new_ session.

Edit hostfiles, edit DNS records --> `/etc/hosts`

su - : create a new session as root.

Who can do sudo? `/etc/sudoers` --> to modify it - use "visudo" instead of sudo. If we see a **%** that means it's a _group_. Check what group you belong to: groups <username>.

| user | which workstattion| = | (which commands) | authenticate? |
| ---- |------ |----- |------ |--------|
| <username/groupname>| ALL| =| (ALL) | ALL|

jdoe    ALL=(ALL)   ALL
jdoe    ALL=(ALL)   NOPASSWD:ALL
%users  ALL=/sbin/mount /mnt/cdrom, /sbin/umont /mnt/cdrom

People on the users group can run mount and umount command cdrom.

Check my group `groups <username>`

- which --> where is that command located

## Managing Users & Groups

- useradd --> add a user. need to be SU. sudo adduser sarah
  - -c --> comment (fullname of the user)
  - -e --> experition date
  - -s --> change shell (/bin/dash)
  - -d --> home folder (/home/jane_smith); needs to be created manually
- sudo id sarah
- sudo userdel <username>: delete user
  - -r removes home directory and files associated
- usermod: modify
  - -c add a comment
  - -l modify the name of the accoumt - sudo usermod -l sjones sarah; the new name for the account is sjones
- passwd <username> : add a password to an account.
- chage --> change user password expiry information
  - chage -l <username>: information about the password

### Default settings when creating an account

useradd -D : see defaults. /etc/skel --> when a new user is created, it takes information from that folder and puts it into the home directory. Modifications only affect new users, not existing users.

`/etc/login.defs` --> login definitions - we got mail box? password age, create home direcotry?+|}

useradd command --> /etc/default check config in there.

/sbin/**nologin** -> have access but not shell

chsh --> change shell

<username>:`X` the x is for the password; we can look at passwords if we look into sudo tail /etc/shadow

In the /etc/shadow we see username + a hash; if they don't have hash, it's because they don't have passwords

| username | hash | date created | starting time | expiration date | warning ahead |
| ------ | ----- |-------- | -------- |--------- |----------|
| zach | ñlakfdjlkñadjfñklajdñfkjasdfk | 17960| 0 | 99999 | 7 |

tail /etc/group --> every time we create a user, we create a group with the same name.

### Groups

Create groups

- sudo groupadd <name>
- sudo groupmod
  - -n change the name (sudo groupmod -n Marketing marketing)
- cat /etc/group
- groupdel

Users have primary group and secondary groups. When we create a user, we create the primary group for that user

- sudo gpasswd -a jdoe Sales : adding a user to Sales
- sudo gpasswd -d jdoe Sales : delete user from Sales
- sudo gpasswd -A jdoe Sales : add jdoe as admin **-A**

When we define a file, we define a User, a group and an other. A user will have certain access to a file, a group, which will usually be a person's primary group may have access to a file and other is anything else.

Establish primary group:

- newgrp Marketing --> do things within another group.
- chgrp

id <username> --> see information on the user

groups --> see the groups you belong to

tail /etc/group

gentent --> find information inside /etc/group and /etc/passwd files.

## File Access & Permissions

## Disk Partitions & File Systems

## Logical Volumes & Filesystem Hierarchy

## Using vi/vim to Edit Files

## Locating & Manipulating Files

## Searching & Manipulating File Contents

## Boot Process & Kernel

## Graphical User Interfaces
