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



* Vulnerability / Attack TTPs references
  * Mitre ATT&CK [https://attack.mitre.org/](https://attack.mitre.org/)
  * Mitre Cloud ATT&CK [https://attack.mitre.org/matrices/enterprise/cloud/](https://attack.mitre.org/matrices/enterprise/cloud/)
  * OWASP TOP 10 [https://owasp.org/www-project-top-ten/OWASP\_Top\_Ten\_2017/](https://owasp.org/www-project-top-ten/OWASP_Top_Ten_2017/)
  * OWASP TOP 10 API [https://www2.owasp.org/www-project-api-security/](https://www2.owasp.org/www-project-api-security/)
  * Mitre CWE [https://cwe.mitre.org/](https://cwe.mitre.org/)
  * NIST [https://nvd.nist.gov/](https://nvd.nist.gov/)
  * Mitre CVE [https://cve.mitre.org/](https://cve.mitre.org/)
  * Mitre CAPEC [https://capec.mitre.org/](https://capec.mitre.org/)
  * Cloud Security Alliance Egregious 11
  * [https://cloudsecurityalliance.org/press-releases/2019/08/09/csa-releases-new-research-top-threats-to-cloud-computi](https://cloudsecurityalliance.org/press-releases/2019/08/09/csa-releases-new-research-top-threats-to-cloud-computi)
  * ng-egregious-eleven/
  * CVSS Score [https://www.first.org/cvss/specification-document](https://www.first.org/cvss/specification-document)
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

### Essential tools

* shodan -
* sshgit - [https://shhgit.darkport.co.uk/](https://shhgit.darkport.co.uk/)
* owasp - [https://owasp.org/](https://owasp.org/)
* trivy - [https://github.com/aquasecurity/trivy](https://github.com/aquasecurity/trivy)
* kube-bench - [https://github.com/aquasecurity/kube-bench](https://github.com/aquasecurity/kube-bench)
* Kubeaudit - [https://github.com/Shopify/kubeaudit/releases/tag/v0.7.0](https://github.com/Shopify/kubeaudit/releases/tag/v0.7.0)
* RhinoLabsCCat - [https://github.com/RhinoSecurityLabs/ccat](https://github.com/RhinoSecurityLabs/ccat)
* CyberArkKubiScan - [https://github.com/cyberark/KubiScan](https://github.com/cyberark/KubiScan)
* github - "k8s.%.com"
* Common Kubernetes ports
* SonarQube.org Code analysis

### Advance

* Watch for container scape → [http://man7.org/linux/man-pages/man7/capabilities.7.html](http://man7.org/linux/man-pages/man7/capabilities.7.html)
  * Cap\_sys\_admin - Perform a range of system administration operations
  * Cap\_sys\_module - Load and unload kernel modules
  * Cap\_sys\_boot - Use reboot\(2\) and kexec\_load\(2\)

Resources

* [https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/\#controlling-access-to-the-kubernetes-api](https://kubernetes.io/docs/tasks/administer-cluster/securing-a-cluster/#controlling-access-to-the-kubernetes-api)
* [https://sysdig.com/blog/33-kubernetes-security-tools/](https://sysdig.com/blog/33-kubernetes-security-tools/)
* [https://www.cisecurity.org/blog/new-cis-benchmark-for-google-cloud-computing-platform/](https://www.cisecurity.org/blog/new-cis-benchmark-for-google-cloud-computing-platform/)
* [https://www.slideshare.net/Lacework/practical-guide-to-securing-kubernetes](https://www.slideshare.net/Lacework/practical-guide-to-securing-kubernetes)
* [https://cloudsecurityalliance.org/press-releases/2019/08/09/csa-releases-new-research-top-threats-to-cloud-computing-egregious-eleven/](https://cloudsecurityalliance.org/press-releases/2019/08/09/csa-releases-new-research-top-threats-to-cloud-computing-egregious-eleven/)
* [https://rhinosecuritylabs.com/aws/cloud-container-attack-tool/](https://rhinosecuritylabs.com/aws/cloud-container-attack-tool/)
* [https://github.com/rsfl/researchdocs/blob/master/Using Splunk\_ELK for Auditing AWS\_GCP\_Azure Security posture - defcon27.pptx](https://github.com/rsfl/researchdocs/blob/master/Using%20Splunk_ELK%20for%20Auditing%20AWS_GCP_Azure%20Security%20posture%20-%20defcon27.pptx)
* [https://www.amazon.com/Google-Cloud-Certified-Associate-Engineer/dp/1119564417/ref=sr\_1\_1?crid=2TGT6926CWROE&keywords=official+google+cloud+certified+associate+cloud+engineer+study+guide&qid=1580317660&sprefix=associate+engineer+%2Caps%2C194&sr=8-1Resources](https://www.amazon.com/Google-Cloud-Certified-Associate-Engineer/dp/1119564417/ref=sr_1_1?crid=2TGT6926CWROE&keywords=official+google+cloud+certified+associate+cloud+engineer+study+guide&qid=1580317660&sprefix=associate+engineer+%2Caps%2C194&sr=8-1Resources)
* [https://www.cyberark.com/threat-research-blog/kubernetes-pentest-methodology-part-2/](https://www.cyberark.com/threat-research-blog/kubernetes-pentest-methodology-part-2/)
* [https://github.com/calinah/learn-by-hacking-kccn/blob/master/Learn by Hacking.pdf](https://github.com/calinah/learn-by-hacking-kccn/blob/master/Learn%20by%20Hacking.pdf)

