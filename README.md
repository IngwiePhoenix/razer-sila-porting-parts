# Razer Sila Porting Parts

This repo contains information extracted from the EOL'd [Razer Sila WiFi "Gaming" Router](https://mysupport.razer.com/app/answers/detail/a_id/3681/~/razer-sila-%7C-rz37-02510-support-%26-faqs).

Long term, I want to port a modern OpenWrt to it. It's a capable box, even has a 4c4t SoC with active cooling and good I/O. So it'd be a waste to trash it o.o

I ignored the DD-dumps I created, for now - they're up to 3GB big. It also seems as this uses A/B booting, meaning that both rootfs and DTB are redundant.

To be exact, take a close look at the dates for p14 and p15:
```
mmcblk0.dd:      DOS/MBR boot sector; partition 1 : ID=0xee, start-CHS (0x0,0,1), end-CHS (0x3ff,255,63), startsector 1, 4294967295 sectors, extended partition table (last)
mmcblk0boot0.dd: data
mmcblk0boot1.dd: data
mmcblk0p1.dd:    ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), statically linked, no section header
mmcblk0p2.dd:    data
mmcblk0p3.dd:    ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), statically linked, no section header
mmcblk0p4.dd:    data
mmcblk0p5.dd:    data
mmcblk0p6.dd:    data
mmcblk0p7.dd:    data
mmcblk0p8.dd:    data
mmcblk0p9.dd:    ELF 32-bit LSB shared object, ARM, EABI5 version 1 (SYSV), statically linked, no section header
mmcblk0p10.dd:   data
mmcblk0p11.dd:   data
mmcblk0p12.dd:   Device Tree Blob version 17, size=3821580, boot CPU=0, string block size=108, DT structure block size=3821120
mmcblk0p13.dd:   Device Tree Blob version 17, size=3821572, boot CPU=0, string block size=108, DT structure block size=3821112
mmcblk0p14.dd:   Squashfs filesystem, little endian, version 4.0, xz compressed, 30296362 bytes, 3891 inodes, blocksize: 262144 bytes, created: Thu May  7 11:59:36 2020
mmcblk0p15.dd:   Squashfs filesystem, little endian, version 4.0, xz compressed, 30292422 bytes, 3891 inodes, blocksize: 262144 bytes, created: Wed Aug 28 11:47:24 2019
mmcblk0p16.dd:   Linux rev 1.0 ext4 filesystem data, UUID=6ba9a62d-f7b9-4db9-bda8-2ff8aebac6ca (needs journal recovery) (extents) (large files) (huge files)
mmcblk0rpmb.dd:  empty
```

Also, the device trees are actually FDTs and I have yet to learn how to break them down into the actual parts of their sum... Still, I would love to document my journey of making this port and hopefuly giving value to those that also have this box just existing somewhere in their cupboard.

# ToDo's:
- [ ] Convert FDT -> DTS + Kernel + extras
- [ ] Disassemble the device
  - [ ] Find JTAG/UART connectors/pins
  - [ ] Document chips and the process of getting there
- [ ] Configure cross-compiling TC
- [ ] Build a kernel (mainline if possible, 6.x; maybe 6.1 because LTS)
- [ ] Build a bootloader
- [ ] Build a whole OpenWrt (24.x probably)
- [ ] Test on own hardware
- [ ] Leverage the `ubus`-"exploit" to create an install script.
  * There is a built-in update script; maybe it can be leveraged.
