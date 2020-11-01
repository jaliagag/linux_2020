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

If there's [] --> optional; if there is no [], that's mandatory.

Using a hyphen when logging in, we are _creating a session_ for that user. You are _fully_ that user; if you don't use the hyphen, you are modifying your session, instead of creating a new session.

su - : create a new session as root.

Who can do sudo? /etc/sudoers --> to modify it - use "visudo" instead of sudo. If we see a **%** that means it's a _group_. Check what group you belong to: groups <username>.

<username/groupname>	ALL=(ALL)	

## Managing Users & Groups

## File Access & Permissions

## Disk Partitions & File Systems

## Logical Volumes & Filesystem Hierarchy

## Using vi/vim to Edit Files

## Locating & Manipulating Files

## Searching & Manipulating File Contents

## Boot Process & Kernel

## Graphical User Interfaces
