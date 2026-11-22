# Bootloader

## Intended architecture

Preserve the existing Mint-managed custom GRUB menu during Nobara to CachyOS migration. Avoid os-prober regeneration unless deliberately changing the design.

## Verification

```bash
sudo efibootmgr -v
findmnt /boot
findmnt /boot/efi
lsblk -f
```

Back up Mint's GRUB configuration, custom menu entries and EFI contents locally. Identify each loader and verify UUIDs against the live inventory. Current configuration pending inspection; no EFI partition is approved for formatting.
