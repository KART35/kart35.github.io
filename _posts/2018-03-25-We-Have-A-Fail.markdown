---
layout: post
title: We Have A Fail!
date: 2018-03-25 22:48:00 -0700
categories: lab ipmi fail
---

If you see this when running `ipmitool`
```
Could not open device at /dev/ipmi0 or /dev/ipmi/0 or /dev/ipmidev/0: No such file or directory
```

Yet you ran it as root, `/dev/ipmi0` exists, and `lsmod` shows all the relevant kernel modules are loaded. Does `dmesg | grep 'ipmi_si'` return something like this?

```
[   11.357376] ipmi_si IPI0001:00: ipmi_si: probing via ACPI
[   11.357400] ipmi_si IPI0001:00: [io  0x0ca2] regsize 1 spacing 1 irq 0
[   11.357402] ipmi_si: Adding ACPI-specified kcs state machine
[   11.357450] ipmi_si: Trying ACPI-specified kcs state machine at i/o address 0xca2, slave address 0x0, irq 0
[   67.052748] ipmi_si: There appears to be no BMC at this location
```

If so, shut down the server. Unplug the server. Wait 30 seconds. Plug it back in. Boot the server.

It will work. This took far too long to figure out.
