BrodyLinux

BrodyLinux is a minimal Linux distribution built manually for educational purposes.

This project exists mainly to understand how Linux works at a low level:
how the kernel boots, how initrd is created, and how a minimal userspace can be assembled from scratch.

This is not a full operating system and not intended for daily use.

Purpose

The goal of this project is learning and experimentation.

While working on BrodyLinux, I wanted to:

understand the Linux boot process (kernel → initrd → init)

build a minimal root filesystem by hand

use BusyBox as a lightweight userspace

create a bootable ISO using isolinux

get a working system that boots directly into a shell

This project is not trying to compete with existing distributions.

What this is

Linux kernel (taken from the host system)

BusyBox-based userspace

initrd-based boot

isolinux bootloader

No graphical interface

After boot, the system drops directly into a shell.

What is included

Bootable ISO

Working init

BusyBox (sh, ls, etc.)

nano text editor

Basic filesystem layout

Mounted /proc, /sys, and /dev

What is NOT included

Networking tools

Package manager

Compiler

Graphical interface

User accounts or security features

These limitations are intentional — this is a learning project.

Building

The ISO is built using a simple shell script.

Requirements:

Linux host system

busybox

isolinux / syslinux

xorriso

cpio

gzip

To build:

chmod +x build.sh
./build.sh


After the build finishes, a bootable ISO image will be created.

Warning

This project is experimental and educational.
Do not use it on real systems or for anything important.

Future ideas

Possible improvements (if the project continues):

basic networking

SSH access

better init system

cleaner build process

documentation of internals

License

This project is released for educational purposes.
Use it, study it, break it, and learn from it.
 Install from Google Drive - https://drive.google.com/file/d/1ZcNziYnOjMObizAca2Ki6euE1K4oQun5/view?usp=drive_link
