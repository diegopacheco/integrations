---
title: collectd df Plugin
brief: Disk Free metrics for collectd.
---

#![](https://github.com/signalfx/integrations/blob/master/collectd/img/integrations_collectd.png) DF (Disk Free) Plugin  

_This is a directory consolidate all the metadata associated with the df collectd plugin. The relevant code for the plugin can be found [here](https://github.com/signalfx/collectd/blob/master/src/df.c)_

- [Description](#description)
- [Requirements and Dependencies](#requirements-and-dependencies)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Metrics](#metrics)
- [License](#license)

### DESCRIPTION

From [collectd wiki](https://collectd.org/wiki/index.php/Plugin:DF):

> The DF plugin collects file system usage information, i. e. basically how much space on a mounted partition is used and how much is available. It's named after and very similar to the df(1) UNIX command that's been around forever.
However, not all "partitions" are of interest. For example /proc and /dev usually don't get filled and their "size" doesn't make a lot of sense. That's why the DF plugin offers to select only specific devices, mount points or filesystem types.

### REQUIREMENTS AND DEPENDENCIES

This plugin requires:

| Software  | Version        |
|-----------|----------------|
| collectd  | 3.6+ |

### INSTALLATION

Installation and initial configuration options are available as part of the [SignalFx collectd agent](https://github.com/signalfx/integrations/tree/master/collectd). 


### CONFIGURATION

Configuration for this plugin is kept in the main [collectd.conf](https://github.com/signalfx/integrations/blob/master/collectd/collectd.conf) file.

| Configuration Option | Type | Definition |
|----------------------|------|------------|
|`Device` | _Device_ | Select partitions based on the `devicename` |
|`MountPoint`| _Directory_|Select partitions based on the mountpoint |
|`FSType`| _FSType_ | Select partitions based on the filesystem type|
|`IgnoreSelected`| _true/false_ |Invert the selection: If set to true, all partitions except the ones that match any one of the criteria are collected. By default only selected partitions are collected if a selection is made. If no selection is configured at all, all partitions are selected|
|`ReportByDevice`| _true/false_ |Report using the device name rather than the mountpoint. i.e. with this false, (the default), it will report a disk as "root", but with it true, it will be "sda1" (or whichever)|
|`ReportInodes`| _true/false_ | Enables or disables reporting of free, reserved and used inodes. Defaults to inode collection being disabled _Enable this option if inodes are a scarce resource for you, usually because many small files are stored on the disk. This is a usual scenario for mail transfer agents and web caches_|
|`ValuesAbsolute`| _true/false_ | Enables or disables reporting of free and used disk space in 1K-blocks. Defaults to true|
|`ValuesPercentage`| _true/false_ | Enables or disables reporting of free and used disk space in percentage. Defaults to false. _This is useful for deploying collectd on the cloud, where machines with different disk size may exist. Then it is more practical to configure thresholds based on relative disk size._|

### USAGE

The primary use of this plugin is to track the available space on the systems filesystems. This can be used to set alerts and thresholds to avoid a filesystem from being filled to capacity.

The [SignalFx collectd plugin](https://github.com/signalfx/integrations/tree/master/collectd-signalfx) computes aggregated utilization metrics based on the output of this plugin you can learn more by looking at the [metrics for the plugin](https://github.com/signalfx/integrations/blob/master/collectd-signalfx/docs/disk.utilization.md).

### METRICS

For documentation of the metrics and dimensions emitted by this plugin, [click here](././docs).

### LICENSE

License for this plugin can be found [in the header of the plugin](https://github.com/signalfx/collectd/blob/master/src/df.c)
