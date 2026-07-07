# Homelab Cluster

A fully automated, production‑grade home datacenter built on Proxmox and Kubernetes.

## Current Status
- [x] Phase 1 – Backup & Preparation
- [ ] Phase 2 – Proxmox Installation
- [ ] Future phases – see [docs/phases/](docs/phases/)

## Hardware
- Ryzen 9 3900X, 64 GB DDR4‑3200
- NVMe storage for virtual machines
- Bulk storage for media and backups

## Purpose
This repository documents the entire build process, from bare‑metal hypervisor to a GitOps‑managed Kubernetes cluster. All configurations are version‑controlled; secrets are never committed.

## Learn More
Detailed step‑by‑step guides are in [docs/phases/](docs/phases/).
