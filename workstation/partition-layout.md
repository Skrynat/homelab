# Partition Layout

Inventory observed 2026-11-21 from Arch Linux. Device names are a snapshot and can change between boots. Five internal drives, 17 partitions. Removable BIOS USB drive deliberately excluded. Unverified roles are not confirmed and no formatting is authorized.

## Physical drives

| Device | Model | Type | Reported size | Nominal capacity |
| --- | --- | --- | --- | --- |
| sda | ST4000VN008-2DR166 (Seagate IronWolf) | HDD | 3.6 TiB | 4 TB |
| sdb | WDC WD10EZEX-08WN4A0 | HDD | 931.5 GiB | 1 TB |
| nvme0n1 | Samsung SSD 970 EVO Plus 1TB | NVMe SSD | 931.5 GiB | 1 TB |
| nvme1n1 | Samsung SSD 990 EVO Plus 1TB | NVMe SSD | 931.5 GiB | 1 TB |
| nvme2n1 | WD PC SN740 SDDPNQD-256G-2006 | NVMe SSD | 238.5 GiB | 256 GB |

## Partitions

Mount points reflect the Arch session only. A dash indicates no reported mount or filesystem/label.

| Partition | Size | Filesystem | Label | Mount | Purpose / status |
| --- | --- | --- | --- | --- | --- |
| sda1 | 16 MiB | — | — | — | Likely Microsoft Reserved; verify type |
| sda2 | 3.4 TiB | NTFS | Storage | /mnt/storageHDD4TB | Main shared storage |
| sda3 | 210.3 GiB | ext4 | — | — | Motion surveillance recordings; created after NTFS recording issues |
| sdb1 | 16 MiB | — | — | — | Likely Microsoft Reserved; verify type |
| sdb2 | 931.5 GiB | NTFS | — | — | Contents unknown |
| nvme0n1p1 | 200 GiB | NTFS | WIN_GAMES | — | Likely Windows games; verify |
| nvme0n1p2 | 250 GiB | NTFS | WIN_2 | — | Purpose unknown |
| nvme0n1p3 | 481.5 GiB | ext4 | LINUX_GAMES | — | Dedicated Linux Steam library used by Nobara |
| nvme1n1p1 | 100 MiB | FAT32 | — | /boot/efi | Active Arch EFI; other loaders unverified |
| nvme1n1p2 | 16 MiB | — | — | — | Likely Microsoft Reserved; verify type |
| nvme1n1p3 | 441.5 GiB | NTFS | — | — | Likely Windows system; verify |
| nvme1n1p4 | 880 MiB | NTFS | — | — | Likely Windows recovery; verify type |
| nvme1n1p5 | 36 GiB | swap | — | [SWAP] | Active swap |
| nvme1n1p6 | 452.3 GiB | ext4 | — | / | Arch Linux root |
| nvme2n1p1 | 512 MiB | FAT32 | — | — | EFI; loader ownership to verify |
| nvme2n1p2 | 117.2 GiB | ext4 | — | — | Linux Mint per historical mapping; verify from Mint |
| nvme2n1p3 | 120.8 GiB | ext4 | nobara-root | — | Nobara root; intended CachyOS replacement, pending final verification |

## Verification

- Verify GPT partition types without mounting.
- Confirm unknown NTFS volume contents from Windows or read-only inspection.
- Boot Mint and Nobara to confirm root, EFI and mount configuration.
- Keep the full UUID/PARTUUID mapping in a local backup; verify the installation target against it before any destructive action. This public inventory omits unique filesystem and partition IDs in accordance with the workstation documentation's public-safety approach.
- Preserve every partition other than the intended Nobara replacement; do not format anything until backups and target are verified.

```bash
lsblk -o NAME,MODEL,SIZE,TYPE,FSTYPE,LABEL,PARTTYPE,PARTTYPENAME,UUID,PARTUUID,MOUNTPOINTS
findmnt --real
sudo fdisk -l
```
