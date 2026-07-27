# Motion Surveillance Troubleshooting

## Permission Denied Under `/srv/motion`

The Motion storage directory is owned by:

```text
motion:motion
````

Example:

```text
drwxr-x--- motion motion /srv/motion
```

A normal administrative user cannot create directories there directly.

Create service-owned directories with:

```bash
sudo -u motion mkdir /srv/motion/storage
```

Check permissions with:

```bash
ls -ld /srv/motion
ls -ld /srv/motion/*
```

## Motion Fails to Start

Check the service status:

```bash
sudo systemctl status motion --no-pager
```

Read recent logs:

```bash
sudo journalctl -u motion -n 50 --no-pager
```

Confirm that the configured recording directory exists and is writable by the `motion` user:

```bash
sudo -u motion test -w /srv/motion/surveillance && echo writable
```

## Recording Numbers Reset After Restart

Motion event counters can reset when the service restarts.

Use timestamp-based filenames instead:

```text
movie_filename %Y-%m-%d_%H-%M-%S
```

Example:

```text
2026-07-27_08-42-16.mkv
```

## New Recordings Are Not Appearing

Confirm Motion is running:

```bash
systemctl is-active motion
```

Check the configured target directory:

```bash
grep -E '^[[:space:]]*(target_dir|movie_filename)' /etc/motion/motion.conf
```

Watch the directory while triggering movement:

```bash
watch -n 1 'ls -lt /srv/motion/surveillance | head'
```
