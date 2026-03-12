# Module 06: Network Security
**Implementation: Infrastructure Hardening and Traffic Inspection**

## 🛡️ Security Architecture
- **Azure Firewall:** `afw-hub-no-01` (Standard SKU)
- **Security Groups:** Network Security Groups (NSGs) & Application Security Groups (ASGs)
- **Segmentation:** Zero-Trust model applied across Web, App, and Data subnets.

## 🏗️ Core Components
1. **Azure Firewall:** Deployed in `AzureFirewallSubnet` (/26).
2. **DNAT Rules:** Port forwarding for SSH/RDP entry points via Firewall Public IP.
3. **Application Rules:** Restricted FQDN access (e.g., `*.microsoft.com`, `*.ubuntu.com`).
4. **ASG Logic:** Used to group Ubuntu 24.04 nodes for simplified rule management.

## 📁 Technical Evidence
- **Topology:** [M06-Sec-Diagram.png](../Assets/M06-Sec-Diagram.png)
- **Firewall Policy:** [M06-Firewall-Rules.json](../Assets/M06-Firewall-Rules.json)

## ⚖️ Implementation Details
- **User-Defined Routes (UDR):** 0.0.0.0/0 traffic forced through Azure Firewall (Hub) for all Spoke subnets.
- **Service Tags:** Utilized for secure Azure service communication (Storage, SQL).

## 🛠️ Configuration Constraints (DDoS Protection)
- **Status:** Deployment of DDoS Network Protection is suspended. 
- **Limitation:** High cost-threshold for Lab environments; focus remains on standard L3/L4/L7 security controls.
