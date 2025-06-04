# ⚙️ K3s Homelab Automation

This project automates the setup and teardown of a lightweight Kubernetes (K3s) cluster across virtual machines provisioned in a homelab, specifically tailored for Proxmox + cloud-init environments.

## 📌 Features
=======
## Kubernetes Homelab

Welcome to my Kubernetes Homelab repository! This is where I document my journey about cloud-native technologies and self-hosting applications. This homelab is more than a playground—it's a platform where I explore ideas, automate workflows, and solve complex challenges while having fun.

As a DevOps Enthusiast, I'm curious about Kubernetes and creating pipelines. This homelab represents my passion for learning and experimenting with technology, with a focus on scalability, backup strategies, and operational simplicity.

## 🚀 Why a Homelab?

- Fully automated K3s installation using Ansible
- One master node and multiple workers
- Traefik disabled (for custom ingress control)
- Clean teardown of the entire cluster
- Easily repeatable installs — great for GitOps workflows

## 🗂 Project Structure
k3s-ansible/
├── inventory/
│   └── hosts.ini         # Define master and worker nodes
├── install-k3s.yml       # Main Ansible playbook to install K3s
├── teardown-k3s.yml      # Optional: Wipe and reset the cluster

<<<<<<< HEAD
## ✅ Requirements
=======
## 🖥️ My Hardware
Beelink Ai Mini PC EQR6 6900HX, synology NAS.

- Proxmox VMs with static IPs and cloud-init SSH access
- SSH public key added to VMs (via cloud-init)
- Ansible installed on your local machine 
- Python 3 available on the target VMs

## 🚀 Usage

### 1. Define Your Inventory

Edit `inventory/hosts.ini`:

```ini
[k3s_master]
10.0.0.202 ansible_user=badex ansible_become=true

[k3s_workers]
10.0.0.203 ansible_user=badex ansible_become=true
10.0.0.204 ansible_user=badex ansible_become=true

[all:vars]
ansible_python_interpreter=/usr/bin/python3

2. Run the Installer
ansible-playbook -i inventory/hosts.ini install-k3s.yml

This will:
	•	Install K3s on the master
	•	Wait for and retrieve the join token
	•	Install K3s on the workers and join them to the cluster

3. Verify the Cluster

SSH into your master node:

run the command: kubectl get nodes

You should see all nodes as Ready.

4. Optional: Teardown the Cluster

To fully remove K3s from all nodes:

ansible-playbook -i inventory/hosts.ini teardown-k3s.yml

⚠️ Warning: This will destroy all workloads and cluster state (e.g., ArgoCD, Rancher, Longhorn, etc.).


What’s Next?

<<<<<<< HEAD
Future enhancements may include:
	•	GitOps bootstrapping with ArgoCD
	•	MetalLB IP range automation
	•	Longhorn and Rancher installs
	•	Dynamic VM provisioning with Terraform
=======
---

## Guest Topology

| VM name        | vCPU | vRAM | Disk | Primary role |
|----------------|------|------|------|--------------|
| `k8s-master`   | 2    | 4 GB | 40 GB | K3s control plane • Argo CD • MetalLB controller |
| `k8s-node1` | 2    | 4 GB | 40 GB | K3s worker |
| `k8s-node2`      | 2    | 4 GB | 40 GB | K3s worker |

*(Spare CPU/RAM intentionally left free for snapshots and future VMs.)*


To prevent the K3s cluster’s LoadBalancer services from ever colliding with DHCP leases on my home network, i first carved out a “static” slice of the LAN’s /24. The router’s DHCP pool was narrowed from 10.0.0.2‑10.0.0.253 to 10.0.0.2‑10.0.0.200, leaving 10.0.0.240‑10.0.0.250 permanently unassigned by DHCP. I then declared that exact block in our IPAddressPool and L2Advertisement resources inside metallb-system, ensuring MetalLB is the only service that can claim those addresses. Whenever a Kubernetes Service is patched to type: LoadBalancer, MetalLB now draws from this reserved pool, advertises the chosen IP via ARP, and the router never tries to hand the same address to a new device—guaranteeing zero IP‑conflict between the cluster and anything else on the network.

## 🔧 Tools and Applications

The homelab runs a variety of applications, deployed using Kubernetes and managed declaratively through GitOps. Here’s an overview of the setup:

Kubernetes: The backbone for workload orchestration, ensuring high availability and scalability.
ArgoCD: Automates deployments and updates via GitOps workflows, keeping the cluster state consistent with repository configurations.
Longhorn: Distributed storage solution for resilient and scalable data management.
Prometheus and Grafana: Monitoring and observability for tracking cluster performance and health.
Kube-Prometheus-Stack: Comprehensive monitoring and alerting stack with Prometheus, Grafana, and Alertmanager.


## 📂 What’s in This Repository?

This repository is structured to organize and simplify the management of my Kubernetes homelab:

apps/: Contains deployment configurations (Helm charts or raw manifests) for each application.
argocd-apps/: Includes ArgoCD-specific application manifests and GitOps configurations for managing deployments declaratively.
cluster/: Defines Kubernetes cluster-wide configurations, such as networking, storage, and infrastructure setup.

## 📈 My Goals

Deepen Kubernetes Knowledge: Dive deep into advanced Kubernetes concepts, such as networking, GitOps or federation.
Enhance Resilience: Design a self-hosted environment with reliable backups and minimal downtime.
Share Knowledge: Document my progress and learnings to help others interested in setting up their own homelab.
>>>>>>> 05981fb8bb4056295203ee068d349f2db0b759b5


This homelab is a work in progress, and I look forward to expanding it further. Feel free to explore the repository, provide feedback, or draw inspiration for your own Kubernetes journey!
