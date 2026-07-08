# Phase 2 – Proxmox Installation & Security Hardening

Proxmox VE 9.2 was installed on the dual‑NVMe pool (ZFS mirror). The 2 TB LVM media pool was preserved and re‑imported.

## What Was Done
- Installed Proxmox VE 9.2 with ZFS RAID 1 on NVMe drives
- Configured static IP (192.168.0.147) and DNS (AdGuard Home)
- Switched to the free community repository (`trixie`)
- Re‑activated the existing media LVM volume group and mounted it at `/mnt/media`
- Created regular user `fetch-admin` with sudo (`rootpw`)
- Hardened SSH: key‑only authentication for Windows, password login disabled
- Added TOTP fallback for phone (temporarily disabled; will be re‑enabled in a future phase)

## Verification
- Proxmox web UI accessible at `https://pve.fetch-server.duckdns.org:8006`
- Media files available at `/mnt/media`
- `vgdisplay` confirms `media_vg` is active
- Phase 1 backup at `/mnt/media/backup/phase1` intact
- `apt update` runs without errors from the community repository

## Notes
- SSH host key was replaced – old keys were removed from client machines
