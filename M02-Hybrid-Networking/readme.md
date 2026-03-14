# 🤝 Module 02: Hybrid Networking (VPN & vWAN)
**Implementation: Encrypted Inter-Site Connectivity & Global Transit Hubs**

## 🏗️ Unit 03: Create and Configure a Virtual Network Gateway
Implementation of an Azure VPN Gateway to establish an IPsec/IKE encrypted tunnel between on-premises infrastructure and the vnet-spoke-no-01.

*   **Gateway Type:** VPN (Route-based).
*   **SKU Pivot:** VpnGw1 utilized over the Basic SKU. Basic Public IPs for VPN Gateways reach end-of-life on January 31, 2026; VpnGw1 is the mandatory professional minimum.
*   **Networking:** Provisioned within the mandatory GatewaySubnet (/27 prefix) to ensure management plane isolation and high-availability overhead.

### ⚖️ VPN Customization Rationale
*   **Route-Based Strategy:** Standardized on Route-based VPNs to enable IKEv2 and Dynamic Routing (BGP). Policy-based VPNs are documented as legacy constraints with limited tunnel support.
*   **Active-Active Redundancy:** Configured dual-gateway instances with two public IPs. This provides a resilient "Zero-Downtime" path for hybrid workloads in the Norway East region.
*   **Ubuntu Performance:** Validated that IPsec encryption overhead does not throttle the burstable CPU capacity of the B2ats_v2 backend nodes.

---

## 🏗️ Unit 07: Create a Virtual WAN by using Azure Portal
Implementation of Azure Virtual WAN (vWAN) to consolidate multiple hybrid connections into a single, unified transit hub.

*   **Architecture:** Hub-and-Spoke. The Virtual Hub acts as the central orchestration point for all regional and global traffic.
*   **SKU:** Standard vWAN (Required for Hub-to-Hub transit and Firewall Manager integration).

### ⚖️ vWAN Customization Rationale
*   **Centralized Transit:** Pivoted to vWAN to eliminate the complexity of manual mesh-peering. Traffic between spokes and on-premises now transits the Hub automatically.
*   **Enterprise Scaling:** Documented vWAN as the primary solution for environments exceeding 30 VPN tunnels, where standard VNet gateways reach architectural limits.

## 🧪 Implementation Testing
1.  **Tunnel Negotiation:** Confirmed successful IKE Phase 1/2 establishment via Azure Connection logs.
2.  **Hub Route Propagation:** Verified that routes from connected spokes are automatically advertised to the VPN gateways within the vWAN Hub.
3.  **Transit Connectivity:** Confirmed "Spoke-to-Spoke" communication across the Hub without requiring manual User Defined Routes (UDRs).

## 🔍 Proof of Work (Technical Evidence)
- **Topology Diagram:** [M02-Hybrid-Diagram.png](../Assets/M02-Hybrid-Diagram.png) 🖼️
- **VPN Connection Status:** az network vpn-connection show --name VPN-to-OnPrem --resource-group RG-AZ-SEC
- **vWAN Hub Status:** az network vwan hub show --name Hub-NorwayEast --resource-group RG-AZ-SEC

## 🧠 Lessons & Conclusions (The "War Log")
*   **Basic SKU Deprecation:** Basic Public IPs and legacy VPN SKUs are documented as non-production-grade. They are excluded from this repository due to their 2026 retirement timeline.
*   **The /27 Mandate:** A /27 subnet is the technical minimum for vWAN/VPN co-existence to support the internal IP overhead of high-throughput gateway appliances.
*   **vWAN Cost Management:** Standard Virtual WAN Hubs incur an hourly charge ($0.25/hr) immediately upon provisioning. This is a critical factor for student/trial tier budget management.
