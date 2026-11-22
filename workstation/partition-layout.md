# Partition Layout

Verified 2026-11-21 using Arch Linux, Nobara, Mint, Windows Disk Management and owner confirmation. Five internal drives, 17 partitions. Removable USB drives excluded.

Device names below reflect the Arch session; Linux NVMe numbering can change between boots. Use the physical drive model and locally recorded UUID/PARTUUID to identify partitions reliably.

```text
DEVICE       SIZE    FSTYPE  LABEL        PURPOSE
sda          3.6T                         Seagate IronWolf 4TB (ST4000VN008-2DR166)
├─sda1        16M                         Microsoft Reserved
├─sda2       3.4T    ntfs    Storage      Main shared storage
└─sda3     210.3G    ext4                 Motion video recordings

sdb        931.5G                         WD Blue 1TB (WD10EZEX-08WN4A0)
├─sdb1        16M                         Microsoft Reserved
└─sdb2     931.5G    ntfs                 Secondary storage / old PC files

nvme0n1    931.5G                         Samsung 970 EVO Plus 1TB
├─nvme0n1p1  200G    ntfs    WIN_GAMES    Windows games
├─nvme0n1p2  250G    ntfs    WIN_2        Additional Windows games
└─nvme0n1p3 481.5G   ext4    LINUX_GAMES  Linux Steam library

nvme1n1    931.5G                         Samsung 990 EVO Plus 1TB
├─nvme1n1p1  100M    vfat                 Main EFI: Mint GRUB and Windows Boot Manager
├─nvme1n1p2   16M                         Microsoft Reserved
├─nvme1n1p3 441.5G   ntfs                 Windows 11 system, page file and crash dump
├─nvme1n1p4  880M    ntfs                 Windows Recovery Environment
├─nvme1n1p5   36G    swap                 Arch Linux swap
└─nvme1n1p6 452.3G   ext4                 Arch Linux root

nvme2n1    238.5G                         WD PC SN740 256GB (SDDPNQD-256G-2006)
├─nvme2n1p1  512M    vfat                 Nobara EFI (Fedora bootloader)
├─nvme2n1p2 117.2G   ext4                 Linux Mint root
└─nvme2n1p3 120.8G   ext4    nobara-root  Nobara Linux root
```

## Mount and boot notes

- Arch: main EFI mounted at `/boot/efi`; physical 36 GiB swap; shared NTFS storage at `/mnt/storageHDD4TB`.
- Nobara: separate 512 MiB EFI; Linux games at `/games/linux`; 8 GiB zram swap.
- Mint: main EFI mounted at `/boot/efi`; independent 2 GiB swapfile; shared storage and both Windows/Linux game volumes (WIN_GAMES and LINUX_GAMES) mounted via fstab, along with Motion storage.
- Default UEFI entry starts Mint's custom GRUB menu on the Samsung 990, which loads Mint, Arch and Nobara directly and chainloads Windows Boot Manager.
- Windows Disk Management confirms the 441.5 GiB system partition and 880 MiB recovery partition; the 36 GiB primary partition displayed there is Arch swap.

## Migration boundary

Only the WD SN740's 120.8 GiB Nobara root is intended for replacement by CachyOS. Preserve all other partitions, including both EFI partitions. Verify the target using the local UUID inventory and backups before formatting.

