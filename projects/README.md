# 🚀 Engineering Project Portfolio  
### By David Joseph Rubio  
Secure Architecture • Automation • Cloud • Networking • IaC

I emphasize strong security, validation, and multi-tool verification practices in every project — ensuring reliable, compliant, and production-ready infrastructure.

This portfolio contains **representative samples** of my engineering work across networking, cloud, automation, and Kubernetes environments.

All sensitive files and full production implementations are kept private for security reasons.

---

# 🔐 PROJECT 1 — Multi-Enclave Network Architecture (Segmentation + Automation)

A secure multi-enclave environment with strict VLAN/VRF segmentation, ACL enforcement, device hardening, centralized logging, and automated provisioning using Ansible.  
Includes a hybrid AWS VPC design mirroring enclave separation in cloud environments.

---

## 🧩 Architecture Highlights
- Segmented enclaves: Restricted, Public, Sensitive  
- ACL-driven traffic filtering  
- Device hardening + secure routing  
- Automated provisioning for routers/switches (Ansible)  
- Hybrid AWS VPC segmentation  

---

## 📁 Representative Code Samples

### **Cisco Router (core-router.cfg)**
hostname CORE-ROUTER
!
interface GigabitEthernet0/0
description Restricted-Enclave
ip address 10.10.0.1 255.255.255.0
!
interface GigabitEthernet0/1
description Public-Enclave
ip address 10.20.0.1 255.255.255.0
!
ip access-list extended ACL-RESTRICTED
permit ip 10.10.0.0 0.0.0.255 any
deny ip any any log
!
logging host <LOG-SERVER>

yaml
Copy code

---

### **Cisco Access Switch (access-switch.cfg)**
hostname ACCESS-SWITCH
vlan 10
name Restricted
vlan 20
name Public
!
interface GigabitEthernet1/0/1
switchport access vlan 10
spanning-tree portfast

yaml
Copy code

---

### **Ansible Playbook (deploy.yml)**
hosts: routers
gather_facts: no
roles:

router

hosts: switches
gather_facts: no
roles:

switch

yaml
Copy code

---

### **AWS VPC (vpc.tf)**
resource "aws_vpc" "enclave_vpc" {
cidr_block = "10.0.0.0/16"
tags = { Name = "Enclave-VPC" }
}

yaml
Copy code

---

# ☁️ PROJECT 2 — AWS CDK + Terraform Deployment ($36/month IaC Architecture)

A cost-optimized AWS environment built using **both** AWS CDK (TypeScript) and Terraform.  
Includes modular VPC, compute, storage, and validation workflows.

---

## 🧩 Architecture Highlights
- CDK: VPC, EC2, S3, CloudFront stacks  
- Terraform: VPC and compute provisioning  
- Modular IaC design  
- Built-in validation layers  
- Runs under ~$36/month  

---

## 📁 Representative Code Samples

### **CDK VPC Stack (vpc-stack.ts)**
import * as cdk from "aws-cdk-lib";
import { Vpc } from "aws-cdk-lib/aws-ec2";

export class VpcStack extends cdk.Stack {
constructor(scope: cdk.App, id: string, props?: cdk.StackProps) {
super(scope, id, props);

new Vpc(this, "MainVpc", {
ipAddresses: { cidr: "10.0.0.0/16" }
});
}
}

yaml
Copy code

---

### **Terraform EC2 Instance (main.tf)**
resource "aws_instance" "web" {
ami = "ami-placeholder"
instance_type = "t2.micro"
tags = { Name = "Terraform-Demo" }
}

yaml
Copy code

---

### **Validation Notes (validation-overview.md)**
Validation Checklist
VPC CIDR and subnet allocation

IAM least-privilege review

Security group rules audit

EC2 + S3 + CloudFront alignment

Monthly cost target: < $36

yaml
Copy code

---

# ⚙️ PROJECT 3 — Kubernetes Automated Deployment + Ansible Integration

A production-style Kubernetes deployment automated through Ansible and Helm, including ingress/TLS routing, persistent storage, and autoscaling.

---

## 🧩 Architecture Highlights
- Automated Kubernetes setup (Ansible)  
- Helm chart deployments  
- TLS-enabled ingress  
- EBS-backed persistent volumes  
- Horizontal Pod Autoscaling (HPA)  

---

## 📁 Representative Code Samples

### **Kubernetes Deployment (deployment.yaml)**
apiVersion: apps/v1
kind: Deployment
metadata:
name: sample-app
spec:
replicas: 2
selector:
matchLabels:
app: sample
template:
metadata:
labels:
app: sample
spec:
containers:
- name: sample
image: nginx:latest

yaml
Copy code

---

### **Kubernetes Ingress (ingress.yaml)**
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: sample-ingress
spec:
rules:

host: placeholder-domain.com

yaml
Copy code

---

### **Persistent Volume Claim (pvc.yaml)**
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: sample-pvc
spec:
accessModes:
- ReadWriteOnce
resources:
requests:
storage: 5Gi

yaml
Copy code

---

### **Ansible Kubernetes Role (main.yml)**
name: Install Kubernetes packages
apt:
name: kubelet
state: present

yaml
Copy code

---

# 🔒 Security Notice

All files in this portfolio contain **safe, representative samples** only.  
Full production configurations, real routing, kubeconfigs, Ansible inventories, IaC modules, certificates, and automation logic remain private in secure development environments.

This ensures:
- Proper security hygiene  
- No exposure of real infrastructure details  
- Compliance with best practices  

---

# ✅ END OF PORTFOLIO  
Thank you for reviewing my engineering work.  
Feel free to reach out with any questions or opportunities.
