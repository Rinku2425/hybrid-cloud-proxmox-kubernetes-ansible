# hybrid-cloud-proxmox-kubernetes-ansible
Hybrid cloud project using Proxmox, Kubernetes (k3s), Ansible, and Oracle Cloud Infrastructure
# 🌐 Hybrid Cloud Infrastructure Project

**Course Project – TriOS College**  
By Rinku Patel  
Completed: May 2025

This project demonstrates how to deploy a hybrid cloud infrastructure using on-premises virtualization (Proxmox) and Oracle Cloud Infrastructure (OCI), automated with Ansible and containerized with Kubernetes (k3s).

---

## 🚀 Project Overview

This architecture includes:

- **Proxmox VE**: Private virtualization platform (on-prem)
- **Ansible**: Configuration management and automation
- **Kubernetes (k3s)**: Lightweight container orchestration
- **Oracle Cloud Infrastructure (OCI)**: Public cloud hosting
- **Backup**: SMB/CIFS integration for system backup

---

## 🧱 System Components

| System        | Description                                    | OS/Tech         | IP Address          |
|---------------|------------------------------------------------|------------------|---------------------|
| Proxmox Host  | Ansible control node, hypervisor               | Proxmox VE       | 192.168.2.230       |
| Web Server    | Apache web server                              | Ubuntu 22.04     | 192.168.2.233       |
| Windows Server| IIS, Python, Chocolatey                        | Windows Server   | 192.168.2.232       |
| Kubernetes VM | Python app deployed via K3s                    | Ubuntu 24.04     | 192.168.2.236       |
| OCI Cloud VM  | Public web service                             | Ubuntu 20.04     | 129.153.49.245      |

---

## 🛠️ Technologies Used

- **Proxmox VE**  
- **Ansible**  
- **Kubernetes (k3s)**  
- **Oracle Cloud Infrastructure (OCI)**  
- **Apache / IIS / Python**  
- **Windows Server Core**  
- **SMB/CIFS backup integration**

---

## 🔒 Security

- Two-Factor Authentication (2FA) on Proxmox
- SSH Key-based access
- Firewall hardening (IPTables and OCI rules)

---

## 📦 Kubernetes Deployment Steps

```bash
# Install k3s
curl -sfL https://get.k3s.io | sh -

# Create namespace
kubectl create namespace pyapp

# Deploy app
kubectl create deployment pyapp --image=jasoneckert/hello-world-python-x86 -n pyapp

# Scale
kubectl scale deployment pyapp --replicas=3 -n pyapp

# Expose via NodePort
kubectl expose deployment pyapp --type=NodePort --port=3333 -n pyapp

# Enable autoscaling
kubectl autoscale deployment pyapp --min=3 --max=6 --cpu-percent=80 -n pyapp
