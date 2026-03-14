# 🧱 Module 01: Azure Virtual Networking
**Implementation: Foundational Segmentation, DNS Orchestration & Global Peering**

## 🏗️ Unit 04: VNet & Subnet Infrastructure
Implementation of the core address space and micro-segmentation strategy for the Norway East regional footprint.

*   **Address Space:** 10.0.0.0/16 (Primary) with logical segmentation for Web, App, and Data tiers.
*   **Gateway Subnet:** Provisioned the mandatory /27 prefix (GatewaySubnet) to support future hybrid co-existence (M02/M03).
*   **Customization Rationale:** Pivoted to a production-grade CIDR plan that avoids overlap with simulated on-premises ranges (192.168.x.x) used in later modules.

---

## 🏗️ Unit 05: DNS Name Resolution
Implementation of localized and custom name resolution to ensure seamless workload discovery.

*   **Logic:** Azure Private DNS Zones combined with Custom DNS server settings for hybrid-readiness.
*   **Private DNS:** Linked private.contoso.com to the VNet to provide auto-registration for the B2ats_v2 Ubuntu nodes.
*   **Customization Rationale:** Configured Custom DNS settings at the VNet level to prepare for M02/M03 hybrid identity (Active Directory) integration, bypassing the limitations of default Azure-provided DNS.

---

## 🏗️ Unit 06: Global VNet Peering
Implementation of high-speed, low-latency transit between disparate virtual networks.

*   **Topology:** Peer-to-Peer (Mesh) and Hub-and-Spoke readiness.
*   **Transit Logic:** Enabled "Allow Gateway Transit" and "Use Remote Gateways" to centralize hybrid connectivity.
*   **Customization Rationale:** Implemented Global VNet Peering to validate cross-region communication (Norway East to North Europe), documenting the sub-millisecond latency vs. the overhead of VPN-based transit.

## 🧪 Implementation Testing
1.  **Micro-Segmentation Audit:** Verified that VMs in separate subnets can communicate via the Azure backbone but are prepared for NSG lockdown (M06).
2.  **DNS Resolve-Check:** Confirmed vm-backend-01.private.contoso.com resolves to its internal 10.x.x.x IP from a peered VNet.
3.  **Peering Throughput:** Validated that peering bandwidth is only limited by the VM SKU (B2ats_v2) and not the peering link itself.

## 🔍 Proof of Work (Technical Evidence)
- **Topology Diagram:** [M01-VNet-Peering.png](../Assets/M01-VNet-Peering.png) 🖼️
- **DNS Resolution:** nslookup webserver01.private.contoso.com
- **Peering Status:** az network vnet peering list --vnet-name VNet-NorwayEast --resource-group RG-AZ-SEC

## 🧠 Lessons & Conclusions (The "War Log")
*   **DNS Inheritance Lag:** Changing DNS settings at the VNet level requires a VM restart (or DHCP renewal) for the B2ats_v2 Ubuntu nodes to recognize the new resolver.
*   **Peering "Transitivity" Myth:** Azure Peering is NOT transitive by default. If VNet A is peered to B, and B to C, A cannot talk to C without a Hub-and-Spoke NVA or vWAN (M02) orchestration.
*   **Overlapping Address Spaces:** Documented the Hard-Kill constraint: VNet Peering is impossible if address spaces overlap. This reinforces the requirement for strict IPAM during Unit 04.
