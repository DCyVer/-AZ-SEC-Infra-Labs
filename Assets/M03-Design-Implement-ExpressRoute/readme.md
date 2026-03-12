# Module 03: Design and Implement Azure ExpressRoute
**Implementation: Circuit Connectivity and Gateway Configuration**

## 🏗️ Architecture Design
- **ExpressRoute Gateway:** `ergw-hub-no-01` (SKU: Standard)
- **Circuit Configuration:** Azure Private Peering
- **Bandwidth Provisioning:** 50 Mbps (Lab Tier)
- **Peering Location:** Amsterdam / London (Primary/Secondary)

## 📁 Technical Evidence
- **Topology:** [M03-ER-Diagram.png](../Assets/M03-ER-Diagram.png)
- **Template:** [M03-ER-Gateway-Config.json](../Assets/M03-ER-Gateway-Config.json)

## ⚖️ Implementation Details
1. **Gateway Integration:** Deployed into the dedicated `GatewaySubnet` (/27) of the Norway East Hub VNet.
2. **Transit Routing:** Configured for VNet-to-VNet transit via the ExpressRoute Gateway.
3. **BGP Logic:** Focused on route advertisement between the simulated On-Prem environment and Azure Private Peering.

## 🛠️ Configuration Constraints
- **Subscription Policy:** Physical cross-connects are restricted on Student/Trial tiers; implementation focused on the Gateway and Peering configuration logic within the Azure Control Plane.
