# Snapshot Script

This repository contains a simple shell script for making a linux snapshot.
For now, the script only tested in system with this specification:
- Init system: systemd
- Bootloader: systemd-boot (formerly known as gummiboot)

For those who use different init system and bootloader, you might want to
change the `restore()` shell function.

To make it more POSIX compliant, the script run on `dash` rather than `bash`
or `sh`. If you does not have `dash` installed, you might want to change the
shebang (`#!/bin/dash`).

## Usage

The script using `mount` command to mounting different partition for the
backup partition, so we need root privilege and make sure you have separate
partition for backup. Here's an example of running the script using `sudo`
(assuming we are in the same directory as the script):
```sh
sudo ./rsync-snapshot backup
```

By default, the script mount the backup partition into root home directory
`/root/backup`. If you want to change this, you need to change this in the
script and also make sure the directory where you mount the backup partition
exist in `exclude.list` file to prevent recursive backup.

The script using `--mkdir` for `mount` command, if you got an error after
message `Mounted /dev/... at ...`, you might want to remove the flag and
create the backup directory manually.

To print the script usage, we can run the script without any arguments, like
this:
```sh
sudo ./rsync-snapshot
```

To check the backup partition, we can use `lsblk` command.

## References

- [Easy Automated Snapshot-Style Backups with Linux and Rsync](http://www.mikerubel.org/computers/rsync_snapshots/).
- [Arch wiki rsync](https://wiki.archlinux.org/title/rsync#As_a_backup_utility).
