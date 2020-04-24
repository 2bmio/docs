---
description: Trouble-Sothing
---

# Trouble

## recovering/downgrade kernel version

```text
# on arch


blkid | grep crypto
cryptsetup luksOpen /dev/sda2 recover
mount /dev/vg0/root /mnt
arch-chroot /mnt

yay -s downgrade
downgrade linux



```

