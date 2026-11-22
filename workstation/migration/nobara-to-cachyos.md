# Nobara to CachyOS Migration

Status: Planning; no destructive actions approved.

- [ ] Verify the complete [partition layout](../partition-layout.md) and bootloader ownership.
- [ ] Identify a backup destination outside the installation target; confirm capacity and mount point.
- [ ] Back up personal files, hidden configuration, application data, local projects, SSH/GPG material and game saves.
- [ ] Save package inventories, mount configuration, custom scripts and relevant system settings.
- [ ] Back up Mint GRUB and EFI files separately.
- [ ] Verify backups and recoverability of local-only files.
- [ ] Confirm Nobara target by UUID, drive identity and partition size.
- [ ] Install CachyOS without formatting unrelated OS, games or EFI partitions.
- [ ] Integrate CachyOS into existing custom GRUB and test each OS.
- [ ] Reinstall applications and selectively restore data; avoid blindly overwriting new distribution configuration.
- [ ] Reconnect game libraries and verify application, GPU and kernel configuration.

Keep sensitive backup contents local, not in this public repository.
