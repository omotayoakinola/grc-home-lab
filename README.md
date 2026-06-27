# GRC Home Lab

Technical GRC validation and compliance monitoring labs, built 
independently to demonstrate hands-on security control deployment, 
risk monitoring, and compliance evidence generation.

This repository documents self-directed technical work that bridges 
GRC theory and practice. Each lab deploys a real tool or control, 
generates live output, and connects the technical findings back to 
GRC principles including risk treatment, control effectiveness, 
compliance mapping, and audit evidence.

---

## Labs

### Lab 1: File Integrity Monitoring with Wazuh
Deployed Wazuh SIEM on Ubuntu to monitor a Windows endpoint for 
unauthorized file changes. Configured real-time syscheck on a 
sensitive financial documents folder, simulated unauthorized activity, 
analysed live dashboard alerts, and mapped findings to SOX, PCI-DSS, 
HIPAA, ISO 27001, and NIST CSF 2.0.

**Tools:** Wazuh 4.12 · Ubuntu (VMware) · Windows  
**Frameworks:** SOX · PCI-DSS · HIPAA · ISO 27001 · NIST CSF 2.0  
**Control type:** Detective control — File Integrity Monitoring

→ [View lab](./wazuh-fim-lab/)

---

## Skills Demonstrated
- Technical control deployment and configuration
- Risk monitoring and control effectiveness validation
- Live security event analysis and interpretation
- Compliance mapping across multiple frameworks
- Audit evidence generation and documentation
- Connecting technical findings to business risk and governance reporting

---

## Tools Used
- **Wazuh 4.12** — Open-source SIEM and security monitoring platform
- **Ubuntu (VMware)** — Wazuh Manager host
- **Windows** — Monitored endpoint with Wazuh Agent
