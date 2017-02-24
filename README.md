Vagrant Virtualbox setup for CS Engine 1.13.1-cs1 on CentOS 7.3
========================

## Download vagrant from Vagrant website

```
https://www.vagrantup.com/downloads.html
```

## Install Virtual Box

```
https://www.virtualbox.org/wiki/Downloads
```

## Download Xenial box
```
vagrant init centos/7
```

## Install Vagrant Plugins
```
vagrant plugin install vagrant-hostsupdater
vagrant plugin install vagrant-multiprovider-snap
```

## Bring up nodes

```
vagrant up centos-node
```

## Configure Devicemapper

After provisioning the node and installing CS Engine it is highly recommended to configure DeviceMapper to use direct-lvm mode in production. The best practice is to provide a spare block device to create a logical volume as a thinpool. In Virtual Box you may manually create a new disk and attach it to the vm. When you run 'fdisk -l' you should be able to see the disks that are available to you:

```
Disk /dev/sda: 42.9 GB, 42949672960 bytes, 83886080 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk label type: dos
Disk identifier: 0x000dc137

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1            2048        4095        1024   83  Linux
/dev/sda2   *        4096     2101247     1048576   83  Linux
/dev/sda3         2101248    83886079    40892416   8e  Linux LVM

Disk /dev/sdb: 5303 MB, 5303697408 bytes, 10358784 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/sdc: 4214 MB, 4214751232 bytes, 8231936 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

[Configure Docker With DeviceMapper](https://docs.docker.com/engine/userguide/storagedriver/device-mapper-driver/#/configure-docker-with-devicemapper)

After properly configuring devicemapper:

```
[vagrant@centos-node ~]$ docker info
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
Server Version: 1.13.1-cs2
Storage Driver: devicemapper
 Pool Name: docker-thinpool
 Pool Blocksize: 524.3 kB
 Base Device Size: 10.74 GB
 Backing Filesystem: xfs
 Data file:
 Metadata file:
 Data Space Used: 19.92 MB
 Data Space Total: 3.997 GB
 Data Space Available: 3.977 GB
 Metadata Space Used: 40.96 kB
 Metadata Space Total: 41.94 MB
 Metadata Space Available: 41.9 MB
 Thin Pool Minimum Free Space: 399.5 MB
 Udev Sync Supported: true
 Deferred Removal Enabled: true
 Deferred Deletion Enabled: true
 Deferred Deleted Device Count: 0
 Library Version: 1.02.135-RHEL7 (2016-09-28)
Logging Driver: json-file
Cgroup Driver: cgroupfs
```

## Stop nodes

```
vagrant halt centos-node
```

## Destroy nodes

```
vagrant destroy centos-node
```
