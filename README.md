## Kubernetes Homelab

Welcome to my Kubernetes Homelab repository! This is where I document my journey about cloud-native technologies and self-hosting applications. This homelab is more than a playground—it's a platform where I explore ideas, automate workflows, and solve complex challenges while having fun.

As a DevOps Enthusiast, I'm curious about Kubernetes and creating pipelines. This homelab represents my passion for learning and experimenting with technology, with a focus on scalability, backup strategies, and operational simplicity. This project automates the setup and teardown of a lightweight Kubernetes (K3s) cluster across virtual machines provisioned in a homelab, specifically tailored for Proxmox + cloud-init environments.


- Fully automated K3s installation using Ansible
- One master node and multiple workers
- Traefik disabled (for custom ingress control)
- Clean teardown of the entire cluster
- Easily repeatable installs — great for GitOps workflows
- Integrated Longhorn for persistent storage with MinIO as a backup target
- MetalLB and cert-manager with DNS-based challenges for proper ingress and SSL termination.



## 🖥️ My Hardware
2 x Beelink Ai Mini PC EQR6 6900HX, Synology NAS.

This combination offers flexibility and low energy consumption while supporting diverse workloads.


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


This homelab is a work in progress, and I look forward to expanding it further. Feel free to explore the repository, provide feedback, or draw inspiration for your own Kubernetes journey!
