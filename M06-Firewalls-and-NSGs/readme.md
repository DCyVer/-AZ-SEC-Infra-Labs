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


# Unit 07: Azure Firewall Standard Implementation 🛡️
**Status:** 🟢 Verified | **Date:** 2026-03-13

## 🏗️ Deployment Architecture
Implementation of a central security hub to enforce L7 traffic inspection for isolated workloads.

![VNet Topology](./00-VNet-Topology.png)
*Figure 1: Hub-Spoke topology showing Srv-Work isolated in Workload-SN.*

### 🛠️ Core Deviations & Optimizations
*   **Standard SKU:** Mandatory for **DNS Proxy** and **FQDN Filtering**.
*   **Spot Compute:** Ubuntu 24.04 on `Standard_D2als_v6` with NVMe (82% cost-efficiency).
*   **Static IP Anchors:** FW-Private: `10.0.1.4` | FW-Public: `51.13.121.146`.

## 🎯 Technical Validation Log

### 1. The Routing Bridge (Task 05)
Forced all egress traffic through the security stack via User-Defined Route (UDR).
![UDR Configuration](./01-UDR-Bridge.png)

### 2. L7 Gate Enforcement (Task 06)
Configured Application Rules for Ubuntu Azure mirrors.
![L7 Rule Overview](./02a-App-Rule-Overview.png)
![L7 Detailed FQDNs](./02b-App-Rule-L7.png)

### 3. Ingress Management (Task 08)
Established secure management path via DNAT (Port 4000 -> 22).
![DNAT Verification](./03-DNAT-Ingress-Verification.png)

### 4. DNS Proxy Handover (Task 09)
Enforced firewall-orchestrated resolution at the NIC level.
![NIC DNS Update](./04-NIC-DNS-Handover.png)

## ⚖️ Final Readiness Check (Task 10)
![L7 Egress Proof](./06-L7-Egress-Verification.png)
*Baseline Failure (470 status) was remediated via wildcard FQDN whitelisting.*

## 🛠️ Reproduction Scripts
```powershell
# DNAT Ingress Mapping
Add-AzFirewallPolicyDnatRule -Name "ssh-ingress" -Protocol "TCP" -SourceAddress "*" -DestinationPort "4000" -DestinationAddress "51.13.121.146" -TranslatedAddress "10.0.2.4" -TranslatedPort "22"

# DNS Handover
$nic = Get-AzNetworkInterface -Name "srv-work992" -ResourceGroupName "Test-FW-RG"
$nic.DnsSettings.DnsServers.Clear()
$nic.DnsSettings.DnsServers.Add("10.0.1.4")
$nic | Set-AzNetworkInterface
