# VPN Gateway

A dedicated Debian LXC running Tailscale as a subnet router for remote access to the homelab LAN.

## Purpose

The gateway provides secure remote access to internal services without exposing them directly to the public Internet.

## Architecture

Remote device
    │
    │ Tailscale
    ▼
vpn-gateway LXC
192.168.50.61
    │
    │ advertises 192.168.50.0/24
    ▼
Homelab LAN

## Configuration

- Platform: Debian LXC on Proxmox VE
- LAN address: 192.168.50.61
- Advertised subnet: 192.168.50.0/24
- IP forwarding enabled
- Tailscale subnet routing enabled
- Authentication keys and account-specific information are not stored in this repository

## Why a Dedicated LXC?

Remote access is separated from application workloads so the VPN gateway can remain available when other virtual machines or services are restarted or modified.

## Security

This repository does not contain:
- Tailscale authentication keys
- private credentials
- public IP addresses
- account identifiers
