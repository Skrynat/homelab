# Homelab Architecture

The homelab uses Proxmox VE to separate infrastructure and application workloads across dedicated virtual machines and LXC containers.

## Current Systems

| System | Type | Purpose |
|---|---|---|
| proxmox-01 | Physical host | Proxmox VE hypervisor |
| minecraft-server | Debian LXC | Minecraft server |
| vpn-gateway | Debian LXC | Tailscale subnet router |
| general-services | Debian VM | General self-hosted services |

## Network

The LAN uses `192.168.50.0/24` with reserved address ranges for infrastructure, Proxmox hosts, guests, client devices, IoT devices, and testing systems.

See [Network Plan](network-plan.md) for the detailed address allocation.

## Design

Services are separated by responsibility so individual workloads can be restarted, upgraded, or troubleshot without unnecessarily affecting other services.
