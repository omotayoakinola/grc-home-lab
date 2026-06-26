# Lab 1: File Integrity Monitoring with Wazuh

## GRC Objective
A risk assessment identified unauthorized modification or deletion 
of sensitive financial documents as a medium-to-high risk. This lab 
implements and validates a detective control to monitor for that risk, 
producing real audit evidence from a live environment.

---

## Lab Architecture

| Component | Host | GRC Role |
|-----------|------|----------|
| Wazuh Manager | Ubuntu (VMware Virtual Platform) | Risk monitoring platform — aggregates and analyses data for reporting |
| Wazuh Agent | Windows (DESKTOP-I0MF0C0) | Control agent — installed on the monitored endpoint |

---

## What I Did
- Deployed Wazuh Manager on Ubuntu running in VMware
- Installed and registered Wazuh Agent on a Windows machine
- Configured File Integrity Monitoring on 
`C:\Users\omotayo\SensitiveFiles` using real-time syscheck
- Simulated unauthorized file activity by creating, modifying, 
and deleting files in the monitored folder
- Monitored and analysed live alerts in the Wazuh FIM dashboard
- Mapped technical findings to GRC principles including control 
evaluation, risk quantification, compliance evidence, and 
management reporting

---

## Live Dashboard Output

**20 FIM events captured across both monitored hosts**

| Timestamp | Agent | Event | Rule ID | Severity |
|-----------|-------|-------|---------|----------|
| Apr 30 @ 13:40:22 | DESKTOP-I0MF0C0 | File deleted | 553 | 7 |
| Apr 30 @ 13:40:02 | DESKTOP-I0MF0C0 | Integrity checksum changed | 550 | 7 |
| Apr 30 @ 13:39:18 | DESKTOP-I0MF0C0 | File deleted | 553 | 7 |
| Apr 30 @ 13:39:18 | DESKTOP-I0MF0C0 | File added to system | 554 | 5 |
| Apr 30 @ 13:38:28 | DESKTOP-I0MF0C0 | File added to system | 554 | 5 |
| Apr 30 @ 10:11:52 | omotayo-VMware-Virtual-Platform | File deleted (x10) | 553 | 7 |

**Key finding:** Rule 550 (Integrity checksum changed) at 13:40:02 
confirms file content was altered, not just accessed. The 
modify-then-delete sequence is consistent with a cover-up attempt 
and would trigger immediate incident response in a production 
environment.

---

## GRC Analysis

**Risk Quantification**
5 FIM events on DESKTOP-I0MF0C0 within a 2-minute window 
(13:38–13:40) directly quantify the risk by frequency, severity, 
and event type. Rule level 7 alerts confirm medium-high severity 
warranting investigation.

**Control Classification**
This FIM implementation is a detective control. Complementary 
preventive controls include Role-Based Access Control with least 
privilege, Data Loss Prevention tooling, and Multi-Factor 
Authentication on the endpoint.

**Compliance Mapping**

| Framework | Requirement | How Wazuh Satisfies It |
|-----------|-------------|----------------------|
| SOX | Monitor integrity of financial reporting controls | FIM alerts on financial documents with tamper-evident logs |
| PCI-DSS | Monitor critical file changes | Real-time syscheck alerts with rule mapping |
| HIPAA | Audit controls for sensitive data | Centralised, timestamped audit trail |
| ISO 27001 | A.12.4 — Logging and monitoring | Centralised log aggregation with retention capability |
| NIST CSF 2.0 | DE.CM — Continuous monitoring | Real-time detection and alerting |

**Audit Evidence Capability**
To demonstrate to an auditor that a specific file was not altered 
during a defined period, the Wazuh Threat Hunting dashboard is 
filtered by `rule.groups: syscheck` and the specific file path. 
No alerts returned confirms integrity. Alerts returned provide an 
itemised change log with timestamps and cryptographic hashes, 
exportable as PDF or CSV for audit packages.

**Management Reporting Metrics**
1. Total FIM alert volume by severity over time
2. Alert breakdown by event type: added, modified, deleted
3. Agent uptime and availability confirming no monitoring gaps

---

## Screenshots

![FIM Dashboard Overview — Alerts by Action Over Time](./screenshots/wazuh_omotayo.PNG)
![FIM Dashboard — Top 5 Agents, Rule Distribution, Actions, Top Users](./screenshots/wazuh_omotayo_1.PNG)
![FIM Events Log — Individual Alerts with Timestamps and Rule IDs](./screenshots/wazuh_omotayo_2.PNG)

---

## Skills Demonstrated
- Technical control deployment and configuration
- Risk monitoring and control effectiveness validation
- Live security event analysis and interpretation
- Compliance mapping across SOX, PCI-DSS, HIPAA, ISO 27001, 
and NIST CSF 2.0
- Audit evidence generation and documentation
- Connecting technical findings to business risk and governance 
reporting

---

## Tools Used
- **Wazuh 4.12** — Open-source SIEM and security monitoring platform
- **Ubuntu (VMware)** — Wazuh Manager host
- **Windows** — Monitored endpoint with Wazuh Agent
- **VMware** — Lab virtualisation environment
