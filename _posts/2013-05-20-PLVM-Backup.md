---
published: true
layout: post
categories:
  - blog
tags:
  - backup
  - lvm
  - partition
---
## What is PLVM-Backup?
PLVM-Backup is a tool to backup/restore of LVM with partitions.

Sometimes, we use an lvm volume as a disk, not a partition. But how we backup/restore them?

Trantect has the same issue when using [iSCSI-Root](/blog/2013/05/20/iSCSI-Root/) in office. In the [iSCSI-Root](/blog/2013/05/20/iSCSI-Root/) system, we use the lvm volume as a block device and make a few partitons on them.
So to make our life more easier, we make this tool to handle the backup/restore tasks.

The source code is hosting on github now: [https://github.com/Trantect/PLVMBackup](https://github.com/Trantect/PLVMBackup)

### Supported filesystems

* ext4
* ntfs

## How to setup?
### Install from ppa

```
sudo add-apt-repository ppa:xiaobo-fei/trantect-lvm-util
```

```
sudo apt-get update
```

```
sudo apt-get install trantect-lvm-util
```

Apologize for the package name in the ppa, we will fix it to PLVM in next version.

### Build from source

```
git clone https://github.com/Trantect/PLVMBackup.git
```

```
cd PLVMBackup
```

```
make install
```

## How to use?
### Backup
Backup volume `/dev/trantect/vol1` to `/mnt/backup/vol1/`.

```
trantect-backup -s 2G /dev/trantect/v1 /mnt/backup/vol1/
```

`-s 2G` meas snapshot size used when backuping.

### Restore
Restore volume `/dev/trantect/vol2` from `/mnt/backup/vol1/`.

```
trantect-restore -l trantect:v2 -d /mnt/backup/vol1
```

### Using with backupninja
Trantect is using backupninja for handle backup tasks. So we write a wrapper script to support backupninja.

Install backupninja first.

```
apt-get install backupninja
```

Link the backupninja wrapper file.

```
ln -s /usr/share/trantect/backupninja/trantect /usr/share/backupninja/trantect
```

Add config file in `/etc/backup.d/20-volume.trantect` with these content.

<pre><code>[lvm]
group = trantect
target_dir = /mnt/backup/
snapshot_size = 2G

volume = vol1
volume = vol2
volume = vol3</code></pre>

This config will let backupninja backup these volumes to `/mnt/backup/`
* /dev/trantect/vol1
* /dev/trantect/vol2
* /dev/trantect/vol3

## Performance
In Trantect, there are 18 volumes whose total size is 600G need to backup. A compete backup task will takes us 90 minutes. And we will get a 250G backup.
