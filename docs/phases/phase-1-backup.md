# Phase 1 – Backup & Preparation

A full backup of the existing Ubuntu Server was created before migrating to Proxmox.

## What Was Done
- All Docker configurations and data (`/srv`) were backed up using `rsync`.
- System configuration files (`fstab`, `blkid`, LVM layout) were saved for reference.
- A sanitized copy of the Docker Compose file will be automatically generated and committed in a future automation step.
- SSH access keys were documented and securely stored off‑server.

## Verification
- The backup is stored at `/mnt/media/backup/phase1/srv` and contains all services.

## Notes
- Storage volumes containing the backup are physically separate from the system drives and will remain untouched during Proxmox installation.
- Future automation will handle secret redaction and portfolio updates.
