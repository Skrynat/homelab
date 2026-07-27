# Homelab

Documentation for my Proxmox-based homelab.

This repository tracks the design, setup, troubleshooting, and future plans for a small self-hosted infrastructure environment used for Linux learning, networking practice, remote administration, game hosting, and future services.

## Goals

* Learn Linux server administration
* Practice networking and remote access
* Host useful services locally
* Build real troubleshooting experience
* Document infrastructure decisions clearly
* Maintain public-safe notes without exposing secrets

## Current Architecture

```text
Proxmox Host
│
├── LXC: Minecraft Server
│   ├── Debian
│   ├── Fabric Minecraft Server
│   ├── Homestead modpack
│   ├── 4 vCPU limit
│   └── 10 GB RAM
│
├── LXC: VPN / Network Services
│   ├── Tailscale subnet router
│   ├── Advertises 192.168.50.0/24
│   ├── WireGuard planned for learning/fallback
│   └── 512 MB
│
├── VM: General Services
│   ├── Debian
│   ├── Docker
│   ├── Motion
│   └── Nginx Proxy Manager planned
│
└── Future
    ├── NAS storage mount
    ├── PoE cameras
    └── RTSP feeds
```

## Design Philosophy

The homelab is built around separation of responsibilities.

Minecraft, VPN access, and general services are separated so that each system can be restarted, changed, or debugged without affecting everything else.

The VPN gateway is planned as a dedicated LXC so remote access remains available even when other services, virtual machines, or workstations are rebooted.

## Public Safety

This repository does not include:

* Passwords
* SSH private keys
* Tailscale auth keys
* API tokens
* Real public IP addresses
* Sensitive domain configuration
* Private service credentials

Configuration files are documented using sanitized examples only.

## Current Services

| Service                 | Type        | Status  |
| ----------------------- | ----------- | ------- |
| Minecraft Server        | Debian LXC  | Working |
| Tailscale Subnet Router | LXC         | Working |
| General Services VM     | Debian VM   | Working |
| Motion                  | Docker / VM | Working |
| Nginx Proxy Manager     | Docker / VM | Planned |

## Future Work

* Add Minecraft backup strategy
* Add Proxmox snapshots before major changes
* Document remote administration workflow
* Add diagrams for network layout
* Add monitoring and uptime checks
