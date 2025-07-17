# Btrfs Snapshot Tools

A collection of shell scripts for creating, maintaining, and using Btrfs
snapshots.


### `btrfs-snapshot`
Create up to a certain number of snapshots (by snapshot directory). Most useful
when run as a cronjob or systemd service/timer.

Usage: `btrfs-snapshot <path> <snapshot-dir> <max-num>`. For example, 
```
btrfs-snapshot / hourly 100
```
creates a snapshot of `/` in `/_snapshots/hourly/<timestamp>`, removes the
oldest snapshot in that directory if there are more than 100, and places a
symlink to the new snapshot in `/_snapshots/all/`.


### `snapshot-recover`
Search through the snapshots contained in `<mount_point>/_snapshots/all/` for
different versions of the file or directory given as `$1`. Present a list of
versions of the file give a prompt to copy user-specified ones to `$PWD`.

Usage: `snapshot-recover <filename>`.


### `subvolume-rm`
Delete a file in a btrfs subvolume, even if it is readonly.

Usage: `subvolume-rm [--quiet] <files>`. For example,
```
subvolume-rm /_snapshots/all/*/home/*/some-dir
```
deletes the directory `some-dir` in every user's home directory in every
snapshot.


### `btrfs-snapshot-chroot`
Create a temporary snapshot of `/`, bind mount appropriate things, and chroot
into it.

Usage: `btrfs-snapshot-chroot [--help] [--no-date] [--snap-name <name>]`

### `btrfs-snapshot-now`
Create a snapshot right now, give it a timestamp, and store it in
`$mount_point/_snapshots/`.

Usage: `btrfs-snapshot-now <path>`.
