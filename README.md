Welcome to my Kubernetes Homelab repository! This is where I document my journey about cloud-native technologies and self-hosting applications. This homelab is more than a playground—it's a platform where I explore ideas, automate workflows, and solve complex challenges while having fun.

As a DevOps Enthusiast, I'm really curious about Kubernetes. This homelab represents my passion for learning and experimenting with technology, focusing on scalability, backup strategies, and operational simplicity.

🚀 Why a Homelab?

The purpose of this homelab is:

Learning by Doing: By self-hosting, I tackle the complexities of deploying and managing real-world applications.
All-in-One Environment: This Kubernetes cluster manages all the applications of my home setup, serving as a single, integrated environment for testing, developing, and automating cloud-native workflows.

🖥️ My Hardware

To keep things simple yet powerful, my homelab runs on the following hardware:


**Apple Mac mini — Late 2014 (Model A1347)**  
* **CPU:** Intel Core i7‑4578U @ 3.0 GHz (2 cores / 4 threads, Turbo 3.5 GHz)  
* **Memory:** 16 GB DDR3 1600 MHz  
* **Storage:** 1 TB SATA SSD (VMFS‑6 datastore)  
* **NIC:** Broadcom 1 GbE (bridged to home LAN 10.0.0.0/24)  
* **Hypervisor:** VMware ESXi 8.0u2 (free license)

---

## Guest Topology

| VM name        | vCPU | vRAM | Disk | Primary role |
|----------------|------|------|------|--------------|
| `k8s-master`   | 2    | 4 GB | 40 GB | K3s control plane • Argo CD • MetalLB controller |
| `k8s-node1` | 2    | 4 GB | 40 GB | K3s worker |
| `k8s-node2`      | 2    | 4 GB | 40 GB | K3s worker |

*(Spare CPU/RAM intentionally left free for snapshots and future VMs.)*


To prevent the K3s cluster’s LoadBalancer services from ever colliding with DHCP leases on my home network, i first carved out a “static” slice of the LAN’s /24. The router’s DHCP pool was narrowed from 10.0.0.2‑10.0.0.253 to 10.0.0.2‑10.0.0.200, leaving 10.0.0.240‑10.0.0.250 permanently unassigned by DHCP. I then declared that exact block in our IPAddressPool and L2Advertisement resources inside metallb-system, ensuring MetalLB is the only service that can claim those addresses. Whenever a Kubernetes Service is patched to type: LoadBalancer, MetalLB now draws from this reserved pool, advertises the chosen IP via ARP, and the router never tries to hand the same address to a new device—guaranteeing zero IP‑conflict between the cluster and anything else on the network.

🔧 Tools and Applications
The homelab runs a variety of applications, deployed using Kubernetes and managed declaratively through GitOps. Here’s an overview of the setup:

Kubernetes: The backbone for workload orchestration, ensuring high availability and scalability.
ArgoCD: Automates deployments and updates via GitOps workflows, keeping the cluster state consistent with repository configurations.
Longhorn: Distributed storage solution for resilient and scalable data management.
Prometheus and Grafana: Monitoring and observability for tracking cluster performance and health.
Kube-Prometheus-Stack: Comprehensive monitoring and alerting stack with Prometheus, Grafana, and Alertmanager.

📂 What’s in This Repository?

This repository is structured to organize and simplify the management of my Kubernetes homelab:

apps/: Contains deployment configurations (Helm charts or raw manifests) for each application.
argocd-apps/: Includes ArgoCD-specific application manifests and GitOps configurations for managing deployments declaratively.
cluster/: Defines Kubernetes cluster-wide configurations, such as networking, storage, and infrastructure setup.

📈 My Goals
Deepen Kubernetes Knowledge: Dive deep into advanced Kubernetes concepts, such as networking, GitOps or federation.
Enhance Resilience: Design a self-hosted environment with reliable backups and minimal downtime.
Share Knowledge: Document my progress and learnings to help others interested in setting up their own homelab.


This homelab is a work in progress, and I look forward to expanding it further. Feel free to explore the repository, provide feedback, or draw inspiration for your own Kubernetes journey!
