---
layout: post
title: "DRBD & mkfs: Wrong medium type while trying to determine filesystem size"
---

# DRBD & mkfs: Wrong medium type while trying to determine filesystem size

## Issue

On a freshly created DRBD block device, mkfs throws an error:

```bash
[adam@data01 ~] mkfs.ext4 /dev/drbd0
mke2fs 1.41.12 (17-May-2010)
mkfs.ext4: Wrong medium type while trying to determine filesystem size
```

## Cause:

The DRBD block device you’re trying to access is configured to act as a Secondary device, which means it cannot be accessed to be read ot to be written to.

The state of your device is kept in /proc/drbd:

```bash
[adam@data01 ~] cat /proc/drbd 
version: 8.3.7 (api:88/proto:86-91)
srcversion: EE47D8BF18AC166BE219757 
 0: cs:Connected ro:Secondary/Primary ds:UpToDate/UpToDate C r----
    ns:0 nr:18104264 dw:18100168 dr:0 al:0 bm:0 lo:1024 pe:0 ua:1025 ap:0 ep:2 wo:b oos:0
```
 
The part ro:Secondary/Primary tells you what both nodes are set to.

Another way to check the role of the block device is with the drbdadm command:

```bash
[adam@data01 ~] drbdadm role <resource>
Secondary/Primary
```

## Solution:

Switch the DRBD block device to Primary using drbdadm:

```bash
[adam@data01 ~] drbdadm primary <resource>
```

This shouldn’t generate any output if it doesn’t encounter any errors.

If you get an error message about multiple primaries:

```bash
0: State change failed: (-1) Multiple primaries not allowed by config
Command 'drbdsetup 0 primary' terminated with exit code 11
```

Then you already have a running master or single-master in your setup, then you need to promote it to primary.

One the current Primary run:

```bash
[adam@data02 ~] drbdadm secondary <resource>
```

and on the current Secodary run:

```bash
[adam@data01 ~] drbdadm primary <resource>
```
