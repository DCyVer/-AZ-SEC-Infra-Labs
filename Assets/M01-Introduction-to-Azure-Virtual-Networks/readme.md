# Module 01: Virtual Networking (VNet)

## 🛠️ Design Strategy
- **Region:** Norway East (Primary)
- **Standard:** RFC 1918 Address Space (10.0.0.0/16)
- **Segmentation:** Multi-tier architecture (Web, App, Data subnets)

## 🏗️ Core Infrastructure
1. **Hub VNet:** `vnet-hub-no-01` (Address: 10.10.0.0/16)
2. **Spoke VNet:** `vnet-spoke-no-01` (Address: 10.20.0.0/16)
3. **Peering:** Bi-directional Gateway Transit enabled.

## 📁 Technical Evidence
- [M01-VNet-Topology.png](../Assets/M01-VNet-Topology.png)
- [M01-Deployment.json](../Assets/M01-Deployment.json)

## ⚖️ Compliance & Deviations
- **Rule XIV:** No Public IPs assigned to backend subnets.
- **Quota Pivot:** West Europe used for overflow testing.