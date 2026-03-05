# chris-soc-homelab
# Chris Robinson — Enterprise SOC Homelab

## Overview
A self-built, enterprise-style security operations environment 
designed to simulate real-world detection engineering, incident 
response, and GRC compliance workflows. Built to develop hands-on 
skills aligned with ISSO, GRC Analyst, and SOC Analyst career 
tracks in federal and defense contractor environments.

**Owner:** Chris Robinson | Former U.S. Army Captain  
**Location:** Colorado Springs, CO  
**LinkedIn:** linkedin.com/in/christionirobinson  
**Clearance Eligible:** Yes  

---

## Network Architecture
> Network diagram in progress — OPNsense firewall, 
> Proxmox virtualization, VLAN-segmented environment

---

## Environment — Asset Inventory

| VM | OS | Role | VLAN | IP |
|---|---|---|---|---|
| DC01 | Windows Server 2022 | AD / DNS / GPO | VLAN 20 | 10.20.0.10 |
| SIEM01 | Ubuntu 22.04 | Wazuh Manager | VLAN 10 | 10.10.0.20 |
| SIEM02 | Ubuntu 22.04 | Splunk | VLAN 10 | 10.10.0.30 |
| FW01 | OPNsense | Firewall / Router | All VLANs | Gateway |
| KALI01 | Kali Linux | Red Team / Testing | VLAN 30 | 10.30.0.10 |

---

## Projects

### Detection Engineering
- [Brute Force Detection & Response](./detection-engineering/brute-force-detection)

### GRC & Compliance
- [NIST SP 800-53 Rev 5 Control Mapping](./nist-800-53-mapping)
- [GPO Hardening — CIS Benchmark](./hardening)

### Vulnerability Management
- [Vulnerability Assessment Report](./vulnerability-management)

---

## Technologies
Proxmox | OPNsense | Windows Server 2022 | Active Directory  
Group Policy Objects | Wazuh | Splunk | Kali Linux | OpenVAS

---

## Certifications

| Certification | Status |
|---|---|
| CompTIA A+ | ✅ Earned |
| CompTIA Network+ | ✅ Earned |
| CompTIA Security+ | ✅ Earned |
| ITIL 4 Foundation | ✅ Earned |
| Microsoft AZ-900 | ✅ Earned |
| CompTIA CySA+ | 🔄 In Progress |

---

## About
Former U.S. Army Quartermaster Officer (Captain) transitioning 
into cybersecurity with a focus on GRC, information assurance, 
and ISSO roles. This homelab documents hands-on implementation 
of enterprise security controls, detection engineering, and 
compliance frameworks aligned to NIST SP 800-53 Rev 5.

**Targeting:** GRC Analyst | Jr. ISSO | Security Compliance Analyst  
Federal contractor and cleared environments preferred.
