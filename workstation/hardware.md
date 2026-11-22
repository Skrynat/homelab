# Hardware

Inventory draft; verify against the running workstation.

| Component | Model / specification |
| --- | --- |
| CPU | Pending verification |
| Motherboard | Pending verification |
| RAM | Pending verification |
| GPU | Pending verification |
| Storage | See [partition layout](partition-layout.md) |
| Power supply | Pending verification |
| Cooling | Pending verification |
| Display | Pending verification |

## Discovery

```bash
lscpu
free -h
lspci -nn
lsblk -d -o NAME,MODEL,SIZE,TRAN
```

Review output before publishing; omit serial numbers.
