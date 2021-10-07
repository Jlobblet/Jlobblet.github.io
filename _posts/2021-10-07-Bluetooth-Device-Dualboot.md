---
layout: post
title: "A Quick Guide to Pairing a Bluetooth Device on Windows and Linux"
---

As the title suggests, this is just a quick guide (for myself as much as anyone else) about pairing a bluetooth device on Windows and Linux.
I'm writing this with dual booting in mind, but it would work for other similar scenarios (such as two separate computers).

Prerequisites
-------------

It's easiest to make the necessary changes from Linux.
The only non-standard tool (I assume you have bluetooth and a text editor already) you'll need is `chntpw`, which is available on most distros.

Unless otherwise stated, Linux commands here are intended to be run from root.

- `apt install chntpw`
- `pacman -S chntpw`
- etc.

If you'd rather retrieve data from the registry on Windows, [PsExec](https://docs.microsoft.com/en-us/sysinternals/downloads/psexec) should allow you to access the necessary values.
 
Pair the device on both operating systems
-----------------------------------------

Since we're going to be editing Linux's copy of the data, pair on Windows first.
Then, pair on Windows.

Copy values from the registry
-----------------------------

This involves extracting various keys from the Windows registry to copy over to Linux.

From Linux
==========

Boot into Linux and mount your Windows partition (`sudo mount /dev/sdX /mnt/Windows`).
If you mount via some other mean (such as the Nautilus GUI) and don't know where that is, use `findmnt /dev/sdX` or just `findmnt`.

From the mount point (e.g. `/mnt/Windows`) go to `Windows/System32/config`.
Now use `chntpw -e SYSTEM`.
The registry is case sensitive and `chntpw` has no tab completion.
Oh well!

Start by using `ls` to find the name of the control set key.
It should be something like `CurrentControlSet` or `ControlSet001`.
Then `cd` to `[ControlSet]\Services\BTHPORT\Parameters\Keys`.
`ls` here, find the adapter MAC address and `cd` to it[^1].

Now `ls` again.
The registry should be one of two shapes:

1. With a DWORD value named after the MAC address of the device.
   [Link to section](#1-dword-value-linkkey).
2. With a key named after the MAC address of the device. 
   - `cd` to this then `ls`.
     There should be various DWORD and QWORD values here that you will need.
   [Link to section](#2-key-ltk-and-irk).

Make a note of the device MAC address here.
Some devices use a rotating MAC address that changes each time it is paired.
You may need to update the MAC address on Linux ([detailed here](#mac-address)).

If neither of these are correct this guide is probably out of date.
Sorry!

#### 1. DWORD value (LinkKey)

Use `hex [MAC]` to print out the contents of the value.
It should be 16 pairs of hex digits.
Remove the spaces from them[^2], [then change the appropriate value on Linux](#linkkey).

#### 2. Key (LTK and IRK)

Use `hex LTK` and `hex IRK` to print out the contents of both values.
These should both be 16 pairs of hex digits.
Remove spaces[^2], then [change the corresponding values on Linux](#ltk-and-irk)

From Windows
============

Start an admin PowerShell session.
Put `PsExec` either on `Path` or in the local directory, then run `PsExec64.exe -s -i regedit` to open the registry editor.

Navigate to `HKEY_LOCAL_MACHINE\SYSTEM\[ControlSet]\Services\BTHPORT\Parameters\Keys\[ADAPTER MAC]\[DEVICE MAC]\`.
Save the data from this directly.
[The steps outlined for Linux](#from-linux) are analogous to the steps here.

Change values
-------------

On Linux, go to `/var/lib/bluetooth/[ADAPTER MAC]/[DEVICE MAC]/`[^1].
Within this directory there should be a file called `info`.

Make a backup first (`cp info info.bak` is sufficient) in case you need your mouse back and can't pair it.

Open `info` with your favourite text editor.

LinkKey
=======

Within `info` there should be a section called `[LinkKey]` with a setting called `Key`.
Replace this key with the one found earlier.

LTK and IRK
===========

Within `info` there are several sections that need paying attention to.
Replace the contents of the file with values from the registry as follows:

| Section                  | Key Name | Registry Value |
|--------------------------|----------|----------------|
| `[SlaveLongTermKey]`     | `Key`    | `LTK`          |
| `[IdentityResolvingKey]` | `Key`    | `IRK`          |
| `[LocalSignatureKey]`    | `Key`    | `CSRK`         |

So far I haven't had to touch any of the other values.

MAC Address
===========

Check the directory of the _device_ (not the adapter!) on your Linux system matches the Windows one.
If not, replace it so that they're the same.

The Windows registry entry for the MAC address will be twelve lower-case hex digits.
Linux expects upper case, with `:` every 2 digits.
Quick snippet to do that for you:  
`(tr '[:lower:]' '[:upper:]' | gawk '{$1=$1}1' FPAT='.{2}' OFS=:) <<< [MAC]`

Restart Bluetooth service
-------------------------

`service bluetooth restart`.

Your device should now pair with Linux using the same configuration as it pairs to Windows.

Notes
-----

[^1]: You can use `bluetoothctl` to find the MAC address of both the adapter and your device.
[^2]: `sed -e 's/ //g'`
