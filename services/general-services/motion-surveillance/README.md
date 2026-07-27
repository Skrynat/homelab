# Motion Surveillance Service

Motion is deployed on a Debian virtual machine hosted by Proxmox VE.

The service uses a Logitech C922 webcam passed through from the Proxmox host to the VM. Motion detects movement, records video locally, and sends event notifications through Telegram.

## Architecture

```text
Proxmox VE host
└── Debian General Services VM
    ├── Motion service
    ├── Logitech C922 via USB passthrough
    ├── Telegram notification script
    └── Dedicated recording storage
        └── /srv/motion
            ├── surveillance/
            └── storage/
````

## Storage Layout

| Path                       | Purpose                      |
| -------------------------- | ---------------------------- |
| `/srv/motion/surveillance` | Active Motion recordings     |
| `/srv/motion/storage`      | Manually archived recordings |

The storage tree is owned by the Motion service account:

```text
motion:motion
```

The administrative user is a member of the `motion` group, allowing recordings to be inspected and copied without changing ownership of the service directories.

## Recording Format

Motion records video in MKV format.

Recordings use timestamp-based filenames:

```text
%Y-%m-%d_%H-%M-%S
```

Example:

```text
2026-07-27_08-42-16.mkv
```

This avoids relying on Motion event numbers, which reset when the service restarts.

## Components

* Proxmox VE
* Debian virtual machine
* Motion
* Logitech C922 Pro Stream Webcam
* Dedicated ext4 storage
* systemd
* SSH key-based remote administration
* Telegram event notifications

## Documentation

* [Setup](setup.md)
* [Maintenance](maintenance.md)
* [Troubleshooting](troubleshooting.md)
* [Sanitized configuration example](config/motion.conf.example)

## Security

This repository does not contain:

* SSH private keys
* Telegram bot tokens
* private chat IDs
* passwords
* public IP addresses
* surveillance recordings
* unsanitized production configuration files

