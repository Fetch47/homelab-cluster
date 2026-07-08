# Homelab Cluster

A fully automated, production‑grade home datacenter built on Proxmox and Kubernetes.

## Current Status
- [x] Phase 1 – Backup & Preparation
- [x] Phase 2 – Proxmox Installation & Security Hardening
- [x] Phase 3 – Media Virtual Machine & Storage Integration
- [ ] Phase 4 – Docker Restoration & Service Migration
- [ ] Phase 5 – Networking & Reverse Proxy (Traefik)
- [ ] Phase 6 – Kubernetes Control Plane
- [ ] Phase 7 – Kubernetes Workers
- [ ] Phase 8 – GitOps & Infrastructure as Code
- [ ] Phase 9 – Observability (Prometheus, Grafana, Loki)
- [ ] Phase 10 – Automation (Terraform + Ansible)
- [ ] Phase 11 – Security Hardening (Cluster‑wide)
- [ ] Phase 12 – Backup & Disaster Recovery

## Hardware
- Ryzen 9 3900X, 64 GB DDR4‑3200
- NVMe storage for virtual machines
- 2 TB HDD media pool (LVM)

## Purpose
This repository documents the entire build process, from bare‑metal hypervisor to a GitOps‑managed Kubernetes cluster. All configurations are version‑controlled; secrets are never committed.

## Learn More
Detailed step‑by‑step guides are in [docs/phases/](docs/phases/).
