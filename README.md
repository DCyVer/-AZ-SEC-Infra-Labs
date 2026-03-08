# AZ-SEC-Infra-Labs
Practical implementation of Azure networking foundations, focusing on connectivity, resolution, and traffic security. Mapping AZ-700 infrastructure configurations to SC-200 security operation requirements.

## 🛠️ Implementation Index: Deviations & Enhancements
*The following solutions were implemented outside the standard lab scope to ensure security consistency and resource efficiency.*

- **Persistent SSH Anchor:** Isolated the **SSH Key Resource** in a standalone `Persistent-Resources-RG`. This prevents credential lockout during VM/Resource Group resets and ensures stable access across modules.
- **Private-Only Architecture:** Disabled all **Public IPs** to enforce a zero-trust routing architecture. Connectivity is validated through the **Azure Serial Console** and internal Private IP paths.
- **Quota & Cost Optimization:** Operates within a strict **4-vCPU regional limit** (`norwayeast`) using `Standard_B2ats_v2` SKUs. Cleanup settings ensure NICs and disks are removed with their VMs.
- **Identity-Forward Configuration:** Enabled **System-Assigned Managed Identities** and **Trusted Launch (vTPM/Secure Boot)** across all nodes to maintain a consistent security baseline.

---

## 🏗️ Network Topology & Configuration Baseline
*The following parameters define the environment baseline to maintain a secure, private-only infrastructure.*

- **Regional Anchor:** `norwayeast` (Primary for all VNet resources).
- **Virtual Network (Hub):** `CoreServicesVnet` (10.20.0.0/16).
- **Virtual Network (Spoke 1):** `ManufacturingVnet` (10.30.0.0/16).
- **Virtual Network (Spoke 2):** `ResearchVnet` (10.40.0.0/16).
- **Gateway Subnetting:** Dedicated `/27` range within each VNet for Gateway Infrastructure.
- **Transit Security:** **S2S IPsec/IKEv2 VPN** (VpnGw1AZ) replacing unencrypted VNet Peering to satisfy **NIS2/BIO2** transit encryption.
- **Compute Tier:** `Standard_B2ats_v2` (Spot-eligible for cost optimization).
- **Identity & Integrity:** Trusted Launch (vTPM/Secure Boot) and System-Assigned Managed Identities enabled on all nodes.

---

## 📁 Directory Structure

### **Track 01: Introduction to Azure Virtual Networks**
- `01-VNet-Architecture/`
  - `Assets/`
    - `01-rg-global-topology.png`
    - `02-hub-vnet-overview.png`
    - `03-mfg-vnet-overview.png`
    - `04-research-vnet-overview.png`
- `02-Name-Resolution/`
  - `Assets/`
    - `01-DNS-Zone-Overview.png`
    - `02-VNet-Links.png`
    - `03-Internal-Resolution.png`
- `03-Global-VNet-Peering/`
  - `Assets/`
    - `01-Vnet-Peering-Connected.png`
    - `02-Vnet-Peering-Topology-PreVM.png`
    - `03-vnet-peering-clean-verification.png`
    - `04-Connection-Troubleshoot.png`

### **Track 02: Design and Implement Hybrid Networking**
- `01-VNet-to-VNet-Gateway/`
  - `README.md`
  - `Assets/`
    - `01-vnet-gateway-effective-routes.png`
    - `02-vnet-gateway-connectivity-test.png`

---

## 📘 Module Summaries
*Technical validation of implemented networking solutions.*

### **Module 04: Private DNS Zones**
- **Technical Evidence:** `01-DNS-Zone-Overview.png`, `02-VNet-Links.png`, `03-Internal-Resolution.png`

### **Module 06: Persistent SSH Anchor**
- **Technical Evidence:** `01-SSH-Key-Resource.png`, `02-Trusted-Launch.png`, `03-Serial-Console-Access.png`

### **Module 08: VNet Peering (Global)**
- **Status:** Architecture superseded by Track 02 VPN Gateway configuration to enforce encryption-in-transit.
- **Technical Evidence:** `01-Vnet-Peering-Connected.png`, `02-Vnet-Peering-Topology-PreVM.png`, `03-vnet-peering-clean-verification.png`, `04-Connection-Troubleshoot.png`

### **Module 02: VNet-to-VNet Gateway**
- **Security Logic:** Migrated from unencrypted peering to an encrypted S2S VPN tunnel to meet **NIS2/BIO2** transit security requirements.
- **Technical Evidence:**
  - `01-vnet-gateway-effective-routes.png` (Routing Table Validation)
  - `02-vnet-gateway-connectivity-test.png` (Data Plane Handshake - Pending)

---

*Note: All private keys (.pem) are stored locally and excluded from this repository via `.gitignore`.*
