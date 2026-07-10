# Network Plan

## LAN

Subnet: `192.168.50.0/24`

Gateway: `192.168.50.1`

## Address Allocation

### Core Infrastructure

`192.168.50.2 - 192.168.50.49`

Reserved for physical infrastructure and future network equipment.

Examples:

* NAS
* Managed switches
* Access points
* Physical servers
* Network appliances

### Proxmox Hosts

`192.168.50.50 - 192.168.50.59`

Reserved for the Proxmox nodes, a.k.a. each ThinkCentre hosting PVE.

| IP            | Host             | Role                    |
| ------------- | ---------------- | ----------------------- |
| 192.168.50.50 | proxmox-01       | Proxmox VE host         |

### Proxmox Guests

`192.168.50.60 - 192.168.50.99`

Reserved for the Proxmox services hosted on the nodes.

| IP            | Host             | Role                    |
| ------------- | ---------------- | ----------------------- |
| 192.168.50.60 | minecraft-server | Minecraft LXC           |
| 192.168.50.61 | vpn-gateway      | Tailscale subnet router |
| 192.168.50.62 | general-services | Docker / service VM     |

### User Devices (DHCP)

`192.168.50.100 - 192.168.50.199`

Dynamic client devices.

Examples:

* Desktop workstation
* Laptop
* Phones
* Tablets
* Guest devices

### IoT and Smart Devices

`192.168.50.200 - 192.168.50.239`

Examples:

* Smart plugs
* Smart speakers
* Cameras
* TVs
* Printers

### Temporary / Testing

`192.168.50.240 - 192.168.50.253`

Reserved for experiments, temporary VMs, and troubleshooting.

### Reserved

`192.168.50.254`

Reserved for future use.

## Remote Access

The VPN gateway advertises:

`192.168.50.0/24`

through Tailscale, allowing remote access to internal services without exposing them directly to the Internet.
