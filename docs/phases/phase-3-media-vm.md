# Phase 3 – Media Virtual Machine & Storage Integration

**Objective:** Create the primary virtual machine that will host all Dockerised services, attach the existing 2 TB media pool, and harden the operating system.

---

## Virtual Machine Provisioning
| Resource | Allocation |
| :--- | :--- |
| **Hypervisor** | Proxmox VE 9.2 |
| **VM ID** | 100 (name: `media-vm`) |
| **CPU** | 4 vCPUs (x86-64-v2-AES, 1 socket) |
| **Memory** | 8 GiB |
| **Boot Disk** | 64 GiB VirtIO Block on `local-zfs` (NVMe pool) |
| **Network** | VirtIO paravirtualised NIC attached to `vmbr0` |

---

## Operating System Installation
- **ISO:** Ubuntu Server 26.04 LTS (live-server)
- **Kernel:** 6.8.0-117-generic
- **Filesystem:** LVM on VirtIO disk (`ubuntu-vg`)
- **Network:** Static IPv4 configuration
  - **IP:** 192.168.0.140/24
  - **Gateway:** 192.168.0.1
  - **DNS:** 192.168.0.148 (AdGuard Home)

---

## Access & Authentication
- **Regular user:** `media-admin` (strong password, sudo enabled)
- **SSH key:** Ed25519 key (`id_fetch_server`) added for password‑less login
- **SSH server:** `PubkeyAuthentication yes` enforced; `PasswordAuthentication` disabled (key‑only)
- **Windows SSH config** updated with `Host media-vm` alias → `192.168.0.140`

---

## 2 TB Media Pool Integration
1. Deactivated LVM volume group `media_vg` on the Proxmox host.
2. Attached the logical volume `/dev/media_vg/media_lv` as `virtio1` to VM 100.
3. Shut down the VM, deactivated the VG on the host, started the VM, then mounted `/dev/vdb` inside the guest.
4. Mount point: `/mnt/media` (contains `backup`, `downloads`, `immich`, `movies`, `nextcloud`, `tv`).
5. Permanent mount added to `/etc/fstab`: /dev/vdb /mnt/media ext4 defaults 0 2

---

## Security Hardening
- **`media-admin` password:** replaced weak initial password with a strong password.
- **Root PIN:** root account password set to a 4‑digit numeric PIN.
- **`sudo` configured with `Defaults rootpw`** – all `sudo` operations now require the root PIN.
- **SSH:** password authentication disabled; only public key authentication permitted.

---

## Verification
- [x] SSH key login from Windows (`ssh media-vm`) works without password.
- [x] `sudo echo "Sudo works with PIN"` prompts for root PIN and succeeds.
- [x] Media pool contents visible at `/mnt/media` after every reboot.
- [x] Proxmox host can still access media pool when the VM is stopped (if re‑attached later).

---

## Notes
- The media pool is dedicated to the Media VM; other VMs will not need direct access.
- Future steps: install Docker Engine, restore service stack from Phase 1 backup, configure firewall.

