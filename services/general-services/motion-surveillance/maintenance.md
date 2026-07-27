# Motion Surveillance Maintenance

## Service Management

Start Motion:

```bash
sudo systemctl start motion
````

Stop Motion:

```bash
sudo systemctl stop motion
```

Restart Motion after changing the configuration:

```bash
sudo systemctl restart motion
```

Check the current service state:

```bash
sudo systemctl status motion --no-pager
```

Check whether Motion is enabled at boot:

```bash
systemctl is-enabled motion
```

Enable it at boot if necessary:

```bash
sudo systemctl enable motion
```

## Viewing Logs

Show recent service logs:

```bash
sudo journalctl -u motion -n 50 --no-pager
```

Follow logs live:

```bash
sudo journalctl -u motion -f
```

Show logs from the current boot:

```bash
sudo journalctl -u motion -b
```

## Storage Layout

```text
/srv/motion/
├── surveillance/   # Active recordings
└── storage/        # Manually archived recordings
```

Check directory sizes:

```bash
sudo du -sh /srv/motion/surveillance
sudo du -sh /srv/motion/storage
```

Check available disk space:

```bash
df -h /srv/motion
```

Count active recordings:

```bash
sudo find /srv/motion/surveillance -type f | wc -l
```

Count archived recordings:

```bash
sudo find /srv/motion/storage -type f | wc -l
```

## Archiving Recordings

Stop Motion before copying active recordings:

```bash
sudo systemctl stop motion
```

Copy all active recordings into the archive directory:

```bash
sudo -u motion cp -av /srv/motion/surveillance/. /srv/motion/storage/
```

Verify that the number of files and approximate directory sizes match:

```bash
sudo find /srv/motion/surveillance -type f | wc -l
sudo find /srv/motion/storage -type f | wc -l

sudo du -sh /srv/motion/surveillance
sudo du -sh /srv/motion/storage
```

Restart Motion after the archive operation:

```bash
sudo systemctl start motion
```

## Clearing Active Recordings

Before deleting recordings, stop Motion and confirm that any required footage has been copied elsewhere:

```bash
sudo systemctl stop motion
```

Delete the contents of the active recording directory while preserving the directory itself:

```bash
sudo find /srv/motion/surveillance -mindepth 1 -delete
```

Verify that the directory is empty:

```bash
sudo ls -la /srv/motion/surveillance
```

Start Motion again:

```bash
sudo systemctl start motion
```

## Checking New Recordings

List the newest recordings:

```bash
sudo ls -lt /srv/motion/surveillance | head
```

Recordings should use timestamp-based names such as:

```text
2026-07-27_08-42-16.mkv
```

## Permissions

The Motion storage tree should remain owned by the Motion service account:

```text
motion:motion
```

Check ownership:

```bash
ls -ld /srv/motion
ls -ld /srv/motion/surveillance
ls -ld /srv/motion/storage
```

Avoid changing the storage tree to the administrative user. Motion should retain ownership of the directories it writes to.
