# Partition Layout

Status: **Pending live verification.** This inventory is not an approved formatting plan.

## Physical drives

| Drive / model | Capacity | Purpose |
| --- | --- | --- |
| Pending | Pending | Pending |

## Partitions

| Device at inventory time | Size | Filesystem | Label | Mount point | OS / purpose | Migration action |
| --- | --- | --- | --- | --- | --- | --- |
| Pending | Pending | Pending | Pending | Pending | Pending | Do not format |

Record every partition including EFI, recovery, reserved, swap and unmounted partitions. Retain a complete UUID/PARTUUID inventory locally and verify it before destructive actions. Device names can change between boots.

## Read-only discovery

```bash
lsblk -o NAME,MODEL,SIZE,TYPE,FSTYPE,LABEL,UUID,PARTUUID,MOUNTPOINTS
sudo fdisk -l
findmnt --real
```

Do not assume unmounted partitions are unused. Confirm the exact installation target and preserve unrelated partitions.
