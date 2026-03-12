# AZ-SEC-Infra-Labs ⚖️ 
Practical implementation of Azure networking foundations, focusing on connectivity, resolution, and traffic security. With a secondary objective to map AZ-700 infrastructure configurations to SC-200 security operation requirements where possible.


## 🛠️ Global Architecture & Constraints
*Strategic deviations implemented to optimize for Azure Trial/Student subscription limits.*

- **Subscriptions:** Azure 1 Trial + Microsoft 365 E5.
- **Region Strategy:** Primary focus on norwayeast (Cost-efficient B-Series availability). Rotated to canadacentral and westeurope to bypass regional Web App quota restrictions.
- **Compute Baseline:** 
  - OS: Ubuntu 24.04 LTS & Windows Server 2019 Datacenter (SmallDisk / x64 / Gen2).
  - Storage: Standard HDD (S4/S6) utilized over Premium SSD for cost-burn optimization.
- **Persistent Logic:** Isolated Persistent-Resources-RG for Public SSH Keys. Enables high-velocity Custom VM ARM Template deployments without credential loss.
- **Zero-Trust Connectivity:** Configurations which did not require Public IP for the objective were executed with private IP VNets/VMs only. Public IPs were strictly constrained to necessary entry-points.
- **Compliance Simulation:** Where applicable simulated requirements for BIO2 / NIS2 compliance.

## 📁 Repository Structure
.
├── Assets/                 # Technical Evidence (PNG/JSON) per Module
├── Docs/                   # Modular Documentation & Unit Deviations
│   ├── M01-VNet.md
│   ├── M02-Hybrid-Networking.md
│   ├── M03-ExpressRoute.md
│   ├── M04-Load-Balancing.md
│   ├── M05-App-Gateway.md
│   └── M06-Network-Security.md
└── README.md               # Root Anchor

## 📁 Implementation Index
- [Module 01: Introduction to Azure Virtual Networks](./Docs/M01-VNet.md)
- [Module 02: Design and Implement Hybrid Networking](./Docs/M02-Hybrid-Networking.md)
- [Module 03: Design and Implement Azure ExpressRoute](./Docs/M03-ExpressRoute.md)
- [Module 04: Design and Implement Azure Load Balancing](./Docs/M04-Load-Balancing.md)
- [Module 05: Design and Implement Azure App Gateway](./Docs/M05-App-Gateway.md)
- [Module 06: Network Security (CURRENT)](./Docs/M06-Network-Security.md)

## ⚠️ Active Blockers
- M06U04 (DDoS): SUSPENDED (Awaiting BreakingPoint Trial License).


## 🛠️ Implementation Index: Deviations & Enhancements
*The following solutions were implemented outside the standard lab scope to ensure security consistency and resource efficiency.*

- **Persistent SSH Anchor:** Isolated the **SSH Key Resource** in a standalone `Persistent-Resources-RG`. This prevents credential lockout during VM/Resource Group resets and ensures stable access across modules.
- **Private-Only Architecture:** Disabled all **Public IPs** to enforce a zero-trust routing architecture. Connectivity is validated through the **Azure Serial Console** and internal Private IP paths.
- **Quota & Cost Optimization:** Operates within a strict **4-vCPU regional limit** (`norwayeast`) using `Standard_B2ats_v2` SKUs. Cleanup settings ensure NICs and disks are removed with their VMs.
- **Identity-Forward Configuration:** Enabled **System-Assigned Managed Identities** and **Trusted Launch (vTPM/Secure Boot)** across all nodes to maintain a consistent security baseline.
- **Regional vCPU Quota Pivot:** Bypassed a terminal **0-vCPU limit for Standard (S1)** in the primary region by pivoting the entire Unit 6 deployment to **West Europe** and **Canada Central** to satisfy multi-regional requirements.
- **Multi-Stage SKU Escalation:** Implemented a two-stage deployment—initially using the **Free (F1)** tier to establish regional presence, followed by a manual upgrade to **Standard (S1)** to satisfy Traffic Manager's backend requirements which are not supported on the Free tier.
- **Application Content Injection (Kudu):** Utilized the **Advanced Tools (Kudu)** console to inject custom **High-Contrast HTML (Blue/Orange)**. This bypassed the generic "Your web app is running" landing page, providing the "Sober Proof" required to visually confirm regional failover in a browser.
- **Layer 7 DNS Validation (Force-Query):** Implemented a **Dual-nslookup Validation** strategy. By forcing queries against **Google DNS (8.8.8.8)** and setting a **1-second TTL**, we bypassed local ISP/Router caching to prove the literal DNS "flip" between West Europe and Canada IPs.

## 🏗️ Network Topology & Configuration Baseline
*The following parameters define the environment baseline to maintain a secure, private-only infrastructure.*

- **Regional Anchor:** `norwayeast` (Primary for all VNet resources).
- **Virtual Networks:** CoreServices (10.20.0.0/16), Manufacturing (10.30.0.0/16), Research (10.40.0.0/16).
- **Transit Security:** **S2S IPsec/IKEv2 VPN** (VpnGw1AZ) and **Virtual WAN Global Transit** replacing unencrypted VNet Peering to satisfy **NIS2/BIO2** transit encryption requirements.
- **Compute Tier:** `Standard_B2ats_v2` (Spot-eligible for cost optimization).
- **L7 Entry Point:** **Azure Application Gateway v2** (Standard) providing a single public VIP for private-only backend pools.
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
  - **M03-Design-Implement-ExpressRoute/**
    - `U04-Configure-Gateway/`
    - `U05-Provision-Circuit/`
  - **M04-Load-Balancing/**
    - `U04-Internal-LB/`
	- `U06-Traffic-Manager/`
  - **M05-Load-Balancing-HTTP/**
    - `U04-Deploy-Azure-Application-Gateway/`
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

### **Module 03: Design and Implement Azure ExpressRoute**
*Establishing high-bandwidth, private-backbone connectivity to bypass public internet risks and satisfy **NIS2/BIO2** isolation requirements.*

#### **Unit 04: Configure an ExpressRoute Gateway**
- **Security Logic:** Deployment of a dedicated `GatewaySubnet` (/27) and ExpressRoute Gateway to anchor private circuit termination.
- **Technical Evidence:** [ExpressRoute-Gateway-Status.png](/Assets/M03-Design-Implement-ExpressRoute/U04-Configure-Gateway/ExpressRoute-Gateway-Status.png) | [ExpressRoute-GatewaySubnet-Proof.png](/Assets/M03-Design-Implement-ExpressRoute/U04-Configure-Gateway/ExpressRoute-GatewaySubnet-Proof.png)
- **Compliance Note:** Subnet sizing (/27) was implemented to support `ErGwScale` and high-availability zone redundancy for future production scaling.

#### **Unit 05: Provision an ExpressRoute Circuit**
- **Security Logic:** Established a private peering circuit via **Telenor (Oslo)** to ensure regional data sovereignty and maintain traffic within the Nordic infrastructure.
- **Technical Evidence:** [ExpressRoute-Circuit-Status.png](/Assets/M03-Design-Implement-ExpressRoute/U05-Provision-Circuit/ExpressRoute-Circuit-Status.png)
- **Key Artifacts:** 
    - **Circuit Status:** Enabled (Azure Resource Active)
    - **Provider Status:** NotProvisioned (Awaiting physical cross-connect / Service Key handshake)
    - **Service Key:** `[REDACTED-GUID]` (Masked per SecOps credential-handling standards).
---

### **Module 04: Load Balancing**
*Implementing high-availability traffic distribution while maintaining a private-only security posture.*

#### **Unit 04: Internal Load Balancer**
- **Security Logic:** Deployment of a Standard Internal Load Balancer (ILB) to provide high availability for backend workloads. By using a private frontend IP, we ensure that zero-trust boundaries are maintained without exposing the pool to the public internet.
- **Technical Evidence:** [01-ilb-curl-validation-load-balance.png](/Assets/M04-Load-Balancing/U04-Internal-LB/01-ilb-curl-validation-load-balance.png)
- **Lessons Learned & Compliance:**
    - **Bastion Developer SKU:** Hard-limit of 1 concurrent connection verified.
    - **ILB Loopback:** Validated that the ILB does not support loopback traffic (source cannot be part of the backend pool if calling the VIP).
    - **Traffic Distribution:** `curl` validation confirms persistent 50/50 distribution across MyVM1 and MyVM2.
	
#### **Unit 06: Azure Traffic Manager**
- **Security Logic:** Implementation of a **DNS-based Global Server Load Balancer (GSLB)** to provide regional failover. This architecture ensures service continuity by routing traffic to the healthiest regional endpoint without a single point of failure at the IP layer.
- **Technical Evidence:** [01-traffic-manager-dns-failover.png](/Assets/M04-Load-Balancing/U06-Traffic-Manager/01-traffic-manager-dns-failover.png) | [02-traffic-manager-endpoint-online.png](/Assets/M04-Load-Balancing/U06-Traffic-Manager/02-traffic-manager-endpoint-online.png)
- **Lessons Learned & Compliance:**
    - **Host Header Sensitivity:** Resolved `400 InvalidUri` errors by utilizing **Azure App Service Endpoints**, which handle host-header negotiation automatically. 
    - **Health Probe Logic:** Successfully transitioned to **HTTPS/443** probing to bypass "HTTPS Only" default App Service redirects.
    - **DNS Caching:** Verified that `nslookup` (Layer 3/4) remains the only **"Sober Proof"** of DNS-level failover due to browser-level TCP socket persistence.

### **Module 05: Design and Implement Azure Load Balancing**
*Simulating real-world legacy constraints and asymmetric traffic distribution.*

#### **Unit 04: Application Gateway & Asymmetric Backends**
- **Regional L7 Transition:** Implementing **Azure Application Gateway** as the regional entry point for Layer 7 traffic routing and SSL termination.
- **Backend Origin Locking:** Enforcing **Network Security Group (NSG)** rules to ensure backends only accept traffic from the Application Gateway Subnet (GatewayManager service tag).
- **Security Logic:** Enforced a **Private-Only NIC** architecture for backend VMs. Traffic is strictly brokered through the Application Gateway; zero direct public exposure.
- **Technical "Pixel-Truth" Deviation:** 
    - **Node Asymmetry:** Deployed a mix of `Standard_D2as_v5` and `Standard_B2als_v2` to test Gateway Health Probe tolerance across varying compute power.
    - **Disk Latency Simulation:** Utilized **Standard HDD** on backends to simulate legacy environment performance under L7 load.
- **Technical Evidence:**
    - `01-load-balance-round-robin.png` (Verification of VM1/VM2 hostname flip-flop via App Gateway).

## 📁 M05 Unit 06: Create Front Door for Highly Available Web Apps
### 📊 Status: Partial Success (Infrastructure Validated / Service Blocked)

Deviation 1: Upgraded to Standard S1 (Curriculum: Free F1) to bypass Kudu file-system restrictions.
Deviation 2: Deployed to Canada Central and West Europe (Curriculum: US Regions) to circumvent subscription-specific quota limits.
Deviation 3: Injected Vexillological Contrast (Blue/Red flags) into index.html to ensure zero-ambiguity during the "Nuclear Failover" test.
Block Log: Azure Front Door aborted (Student Tier restriction). Documented with MS Q&A 1729771.


#### 🛠️ Executed Configuration
- **Region A:** West Europe (Standard S1) - [Blue/Gold Theme]
- **Region B:** Canada Central (Standard S1) - [Red/White Theme]
- **Validation Method:** Custom `index.html` injection via Kudu CMD.

#### ⚠️ Deployment Restriction
The Azure Front Door (Standard) deployment phase was halted due to subscription-level 
entitlement constraints. 
Even upgrading to pay as you go would not grant access: https://learn.microsoft.com/en-us/answers/questions/1729771/unbale-to-create-azure-front-door-service-with-azu

### 📝 EXTERNAL REFERENCE & BLOCK JUSTIFICATION
The Azure Front Door deployment was aborted due to platform-level entitlement 
restrictions on 'Free Trial' and 'Student' subscriptions. 

**Source:** [Microsoft Q&A - Unable to create Azure Front Door with Student Subscription](https://learn.microsoft.com)

**Status Note:** As of late 2024, Microsoft has tightened 'Microsoft.Cdn' 
resource creation to mitigate service abuse. This renders this specific 
unit non-viable for student-tier sandboxes without a transition to 
a seasoned 'Pay-As-You-Go' account.

**Diagnostic Data:**
- **Error Code:** `BadRequest`
- **Root Cause:** Microsoft policy 2024/2025 restricts Azure Front Door / CDN resource 
  creation on 'Free Trial' and 'Student' subscriptions to prevent service abuse.
- **Resolution Path:** Requires conversion to a paid 'Pay-As-You-Go' subscription 
  with established billing history.

#### ⚖️ Learning Outcomes
1. **Multi-Region SKU Parity:** Successfully scaled disparate regional nodes to 
   Standard S1 to support production-level health probes.
2. **Kudu Service Management:** Verified manual file-system injection to differentiate 
   regional endpoints for failover testing.
3. **Global Edge Governance:** Identified specific 'Microsoft.Cdn' provider requirements 
   and subscription-tier limitations.

### 📝 ADR-M05-FINAL: Load Balancing HTTP(S) Deviations
- **SKU Pivot:** Upgraded to **Standard S1** (Curriculum: F1) to enable Kudu file-system write access.
- **Regional Swap:** Deployed to **Canada Central / West Europe** (Curriculum: US) to bypass Student subscription quota limits.
- **Identity Injection:** Custom **Vexillological Contrast** (Blue/Red flags) injected via Kudu for failover verification.
- **Platform Block:** **Azure Front Door** deployment aborted. Root Cause: Student Tier restriction (Ref: MS Q&A 1729771).

---
*Note: All private keys (.pem) are excluded from this repository via .gitignore.*
