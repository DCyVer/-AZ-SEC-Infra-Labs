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
- **Virtual Networks:** CoreServices (10.20.0.0/16), Manufacturing (10.30.0.0/16), Research (10.40.0.0/16).
- **Transit Security:** **S2S IPsec/IKEv2 VPN** (VpnGw1AZ) and **Virtual WAN Global Transit** replacing unencrypted VNet Peering to satisfy **NIS2/BIO2** transit encryption requirements.
- **Compute Tier:** `Standard_B2ats_v2` (Spot-eligible for cost optimization).

---

## 📁 Directory Structure
- **Assets/** (Global Root - Mirrored Structure)
  - **M01-Introduction-to-Azure-Virtual-Networks/**
    - `U04-VNet-Architecture/`
    - `U06-Name-Resolution/`
    - `U08-Global-Peering/`
  - **M02-Design-and-implement-hybrid-networking/**
    - `U02-VNet-to-VNet-Gateway/`
    - `U07-Virtual-WAN-Integration/`

---

## 📘 Module & Unit Summaries
*Technical validation and security logic for implemented networking solutions.*

### **Module 01: Introduction to Azure Virtual Networks**
*Establishing the zero-trust foundation through isolated VNet boundaries and internal resolution.*

#### **Unit 04: VNet Architecture**
- **Security Logic:** Multi-VNet baseline establishing isolated boundaries for Core, Manufacturing, and Research workloads.
- **Technical Evidence:** [01-rg-global-topology.png](/Assets/M01-Introduction-to-Azure-Virtual-Networks/U04-VNet-Architecture/01-rg-global-topology.png)
- **Infrastructure Assets:** [CoreServicesVnet.json](/Assets/M01-Introduction-to-Azure-Virtual-Networks/U04-VNet-Architecture/CoreServicesVnet.json) | [ManufacturingVnet.json](/Assets/M01-Introduction-to-Azure-Virtual-Networks/U04-VNet-Architecture/ManufacturingVnet.json)

#### **Unit 06: Name Resolution**
- **Security Logic:** Implementation of **Azure Private DNS Zones** linked to all regional VNets, eliminating the need for public DNS exposure.
- **Technical Evidence:** [01-nslookup-validation.png](/Assets/M01-Introduction-to-Azure-Virtual-Networks/U06-Name-Resolution/01-nslookup-validation.png) | [02-private-dns-link.png](/Assets/M01-Introduction-to-Azure-Virtual-Networks/U06-Name-Resolution/02-private-dns-link.png)

#### **Unit 08: Global Peering**
- **Security Logic:** Validated L3 reachability between regions. Note: This architecture was superseded by Track 02 encrypted transit to meet compliance.
- **Technical Evidence:** [01-Vnet-Peering-Connected.png](/Assets/M01-Introduction-to-Azure-Virtual-Networks/U08-Global-Peering/01-Vnet-Peering-Connected.png) | [03-vnet-peering-clean-verification.png](/Assets/M01-Introduction-to-Azure-Virtual-Networks/U08-Global-Peering/03-vnet-peering-clean-verification.png)

---

### **Module 02: Design and Implement Hybrid Networking**
*Migrating to encrypted, policy-driven transit to satisfy **NIS2/BIO2** requirements.*

#### **Unit 02: VNet-to-VNet Gateway**
- **Security Logic:** Transitioned from unencrypted peering to an encrypted **S2S IPsec/IKEv2 VPN tunnel** for inter-VNet traffic.
- **Technical Evidence:** [01-vnet-gateway-effective-routes.png](/Assets/M02-Design-and-implement-hybrid-networking/U02-VNet-to-VNet-Gateway/01-vnet-gateway-effective-routes.png) | [03-vnet-gateway-tracepath-nc-success.png](/Assets/M02-Design-and-implement-hybrid-networking/U02-VNet-to-VNet-Gateway/03-vnet-gateway-tracepath-nc-success.png)

#### **Unit 07: Virtual WAN Integration**
- **Security Logic:** Implementation of **Global Transit Architecture** using Azure Virtual WAN to centralize the control plane and spoke connectivity.
- **Technical Evidence:** [01-vwan-insights-topology.png](/Assets/M02-Design-and-implement-hybrid-networking/U07-Virtual-WAN-Integration/01-vwan-insights-topology.png) | [02-vwan-effective-routes.png](/Assets/M02-Design-and-implement-hybrid-networking/U07-Virtual-WAN-Integration/02-vwan-effective-routes.png)

---
*Note: All private keys (.pem) are excluded from this repository via .gitignore.*
