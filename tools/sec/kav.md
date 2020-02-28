---
description: Kubernetes Attack Vectors
---

# KAV



| INTERNAL \(Inside Cluster\) | EXTERNAL \(Outside Cluster\) |
| :--- | :--- |
| CI/CD Devops attack surface \(Accounts, Pods, Nodes\) | Exposed API |
| Application Vulns\(CVE-2019-16276\) | Exposed Kubelet |
| Container Implantation \(Mitre T1147\) | Information disclosure |
| - | Exposed Management GUI |
|  | Denial of Service |



* **Accessing Kubernetes**
  * Transport Security - \(API 6443\)
  * Authentication - Client Certificates, Password, and Plain Tokens, Bootstrap
  * Tokens, and JWT Tokens \(used for service accounts\)
  * Authorization - ABAC mode, RBAC Mode, and Webhook
  * Admission Control - Admission Control Modules are software modules that
  * can modify or reject requests.They act on objects being created, deleted,
  * updated or connected \(proxy\).
  * API Server Ports and IPs - \(8080, 6443, 443\)
* **Kubernetes - The CI/CD - Devops attack surface**
  * Source Code repository: github, gitlab, S3, SVN
  * CI/CD Platform: Jenkins, CircleCI, TravisCI
  * Container Repository: Docker, Vagrant
  * IaaS Provider: Kubernetes flavor, Microsoft EKS, Amazon
  * AKS
  * IaC: Ansible, Terraform, Cloudformation, Chef

