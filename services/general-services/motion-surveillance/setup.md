# Motion Surveillance Setup

## Overview

Motion runs as a systemd service inside the Debian General Services VM on Proxmox VE.

A Logitech C922 webcam is passed through from the Proxmox host to the VM. Motion detects movement and stores recordings under `/srv/motion/surveillance`.

## Storage Structure

```text
/srv/motion/
├── surveillance/   # Active recordings
└── storage/        # Archived recordings
````

The directories are owned by the Motion service account:

```text
motion:motion
```

## Create the Storage Directories

```bash
sudo -u motion mkdir -p /srv/motion/surveillance
sudo -u motion mkdir -p /srv/motion/storage
```

Verify ownership:

```bash
ls -ld /srv/motion
ls -ld /srv/motion/surveillance
ls -ld /srv/motion/storage
```

## Recording Filename Format

In `/etc/motion/motion.conf`:

```text
target_dir /srv/motion/surveillance
movie_filename %Y-%m-%d_%H-%M-%S
```

Example output:

```text
2026-07-27_08-42-16.mkv
```

Timestamp-based filenames are used because Motion event counters reset when the service restarts.

## Start and Verify Motion

```bash
sudo systemctl start motion
sudo systemctl status motion --no-pager
```

Check newly created recordings:

```bash
sudo ls -lt /srv/motion/surveillance | head
```

Inspect service logs if startup fails:

```bash
sudo journalctl -u motion -n 50 --no-pager
```
