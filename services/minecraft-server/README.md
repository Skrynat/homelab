# Minecraft Server

## Overview

This service hosts a modded Minecraft Java Edition server running the Homestead modpack.

The server runs inside a Debian LXC container on a Proxmox VE host and is managed remotely using SSH and tmux.

## Service Information

| Property           | Value         |
| ------------------ | ------------- |
| Type               | LXC Container |
| Host Platform      | Proxmox VE    |
| Operating System   | Debian        |
| Minecraft Version  | 1.20.1        |
| Mod Loader         | Fabric        |
| Modpack            | Homestead     |
| vCPU Limit         | 4             |
| Memory             | 6 GB          |
| Remote Management  | SSH           |
| Console Management | tmux          |

## Purpose

The primary goals of this service are:

* Learn Linux server administration
* Learn Proxmox container management
* Learn remote administration workflows
* Host a persistent multiplayer Minecraft world
* Practice troubleshooting and documentation

## Architecture

```text
Proxmox Host
│
└── Minecraft Server (LXC)
    ├── Debian
    ├── Fabric
    ├── Homestead
    ├── SSH
    └── tmux
```

## Deployment Notes

The server was deployed using a dedicated Debian LXC container.

The Homestead client files were copied from an existing Prism Launcher installation and adapted for server use.

Client-only mods were removed after reviewing Fabric startup logs.

## Troubleshooting

### Client-only Mod Crash

**Issue**

Server failed to start after copying the modpack.

**Cause**

A client-only Fabric mod attempted to load on the server.

**Resolution**

Removed the incompatible client-side mod from the server's mods directory.

## Future Improvements

* Configure automatic startup using systemd
* Implement automated backups
* Integrate Tailscale remote access
* Add monitoring and resource tracking
* Document recovery procedures
