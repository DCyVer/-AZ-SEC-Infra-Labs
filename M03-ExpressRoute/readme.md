# 🚂 Module 03: Azure ExpressRoute
**Implementation: Private Enterprise Connectivity & Dedicated Hybrid-Cloud Backhaul**

## 🏗️ Unit 04: Configure an ExpressRoute Gateway
Implementation of the managed gateway resource to terminate the ExpressRoute circuit within the vnet-spoke-no-01.

*   **Gateway Subnet:** Provisioned the mandatory GatewaySubnet (minimum /27) to host the ExpressRoute appliances.
*   **Gateway Type:** Explicitly set to ExpressRoute. Optimized for throughput rather than the IPsec encryption overhead found in VPN Gateways.

### ⚖️ Gateway Customization Rationale
*   **Dedicated Throughput:** Selected the High-Performance (or Standard) SKU to match the circuit's performance profile, avoiding CPU bottlenecks during high-burst data transfers.
*   **FastPath Evaluation:** Documented the requirement for FastPath to bypass the gateway for direct MSEE-to-VM communication, reducing latency for mission-critical compute.

---

## 🏗️ Unit 05: Provision an ExpressRoute Circuit
Implementation of the Layer 2 circuit between Azure edge locations and the service provider (Equinix/Megaport).

*   **Logic:** Private Peering for internal VNet integration and Microsoft Peering for PaaS/SaaS services.
*   **Provisioning State:** Verified the circuit status transitions from "Not Provisioned" to "Provisioned" via the Service Provider handshake.

### ⚖️ Circuit Customization Rationale
*   **Service Provider Handshake:** Documented the required 3-way handshake (Azure -> Provider -> Customer) via the unique Service Key.
*   **Layer 3 BGP:** Utilized Border Gateway Protocol (BGP) for dynamic route exchange, replacing static routing with an industry-standard protocol for on-premises sync.

## 🧪 Implementation Testing
1.  **ARP Table Audit:** Validated Layer 2 connectivity by inspecting MSEE (Microsoft Enterprise Edge) ARP tables.
2.  **Circuit Connection:** Successfully linked the VNet Gateway to the Circuit using a dedicated Connection resource and authorization key.
3.  **Effective Route Audit:** Verified on-premises network prefixes are correctly appearing in the Azure VNet route table.

## 🔍 Proof of Work (Technical Evidence)
- **Topology Diagram:** [M03-ER-Diagram.png](../Assets/M03-ER-Diagram.png) 🖼️
- **Circuit Status:** az network express-route show --name ER-Circuit-01 --resource-group RG-AZ-SEC
- **BGP Peer Status:** az network vnet-gateway list-bgp-peer-status --name ER-Gateway --resource-group RG-AZ-SEC

## 🧠 Lessons & Conclusions (The "War Log")
*   **Provider Lag:** ExpressRoute deployment involves physical cross-connects and service-key handshakes that can take significantly longer than VPNs.
*   **Billing Mandate:** Documented that ER circuits incur costs the moment the Service Key is generated, regardless of whether traffic is flowing.
*   **Gateway Coexistence:** Documented the routing preference logic where ExpressRoute is prioritized over S2S VPN by default unless specific Weight or AS-Path attributes are manipulated.
