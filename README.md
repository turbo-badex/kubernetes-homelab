# ⚙️ K3s Homelab Automation with Ansible

This project automates the setup and teardown of a lightweight Kubernetes (K3s) cluster across virtual machines provisioned in a homelab — specifically tailored for Proxmox + cloud-init environments.

## 📌 Features

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

## ✅ Requirements

- Proxmox VMs with static IPs and cloud-init SSH access
- SSH public key added to VMs (via cloud-init)
- Ansible installed on your local machine (e.g. via `brew install ansible` on macOS)
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

Future enhancements may include:
	•	GitOps bootstrapping with ArgoCD
	•	MetalLB IP range automation
	•	Longhorn and Rancher installs
	•	Dynamic VM provisioning with Terraform

