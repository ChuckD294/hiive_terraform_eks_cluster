# Hiive DevOps Assessment – EKS Deployment with Terraform

This project provisions a complete AWS EKS environment using Terraform, including a VPC, IAM roles, and Kubernetes resources to run a public NGINX service.

---

## 📦 Project Structure

```
.
├── main.tf                 # Root Terraform entrypoint
├── vpc/                    # VPC, subnets, internet gateway, routes
├── eks/                    # EKS cluster, IAM roles, node group
├── k8s/                    # Kubernetes deployment (NGINX + LoadBalancer)
├── scripts/                # Helper script to configure kubectl
```

---

## 🚀 End-to-End Deployment Instructions

### Prerequisites
- AWS CLI installed and configured (`aws configure`)
- Terraform >= 1.3
- kubectl installed

---


---

### 1. Initialize Terraform

```bash
terraform init
```

---

### 2. Apply Infrastructure

```bash
terraform apply -auto-approve
```

This will create:
- VPC with internet gateway and public subnets
- EKS cluster with IAM roles and managed node group

---

### 3. Configure kubectl

```bash
bash scripts/setup_kubeconfig.sh
kubectl get nodes
```

---

### 4. Deploy the Application

```bash
kubectl apply -f k8s/deployment.yaml
kubectl get svc nginx-service
```

Copy the `EXTERNAL-IP` from the output and open it in a browser.

---

## 🔗 Live Service

**URL**: http://ab53df37911b4fbf58880e1e805a80f4-2107721584.us-east-1.elb.amazonaws.com

**Screenshot**:  
![NGINX Running](./screenshot.png)

---

## 🛠️ Design Decisions

- **Modular Structure**: Code is split into `vpc` and `eks` modules for reusability and clarity.
- **Minimal Public App**: Used NGINX to validate cluster and service exposure quickly.
- **Networking**: Subnets are public with internet access to simplify bootstrapping and LoadBalancer use.
- **IAM Roles**: Cluster and node IAM roles are independently defined and correctly attached with necessary AWS-managed policies.

---

## ✅ Outputs

- EKS Cluster Endpoint
- `aws eks update-kubeconfig` command
- Public NGINX LoadBalancer URL

---
