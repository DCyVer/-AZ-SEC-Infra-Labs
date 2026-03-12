# Module 02: Hybrid Networking (S2S VPN)

## 🏗️ Architecture
- **Hub Gateway:** `vpngw-hub-no-01` (Route-based)
- **Local Network Gateway:** `lng-onprem-no-01` (Simulated On-Prem Endpoint)
- **Encryption:** IKEv2 / IPsec Tunneling

## 🔐 Security Configuration
- **Authentication Method:** Pre-shared Key (PSK)
- **Secret Management:** Manual entry (Non-persistent in documentation per Rule XIV)
- **Network Protection:** NSG rules restricted to UDP 500/4500 on GatewaySubnet

## 📁 Technical Evidence
- [M02-Hybrid-Topology.png](../Assets/M02-Hybrid-Topology.png)
- [M02-Gateway-Status.json](../Assets/M02-Gateway-Status.json)

## ⚖️ Implementation Notes
- **Subnetting:** Dedicated `GatewaySubnet` (/27) in Norway East Hub.
- **Connectivity:** Verified via "Connected" status in Azure Portal (Ref: MS Learn Exercise).
Use code with caution.




