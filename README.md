# AZ-SEC-Infra-Labs
Practical implementation of Azure networking foundations, focusing on connectivity, resolution, and traffic security. Mapping AZ-700 infrastructure configurations to SC-200 security operation requirements.

## 🛠️ Implementation Index: Deviations & Enhancements
*The following solutions were implemented outside the standard lab scope to ensure security consistency and resource efficiency.*

*   **Persistent SSH Anchor:** Isolated the **SSH Key Resource** in a standalone `Persistent-Resources-RG`. This prevents credential lockout during VM/Resource Group resets and ensures template reliability.
*   **Private-Only Architecture:** Disabled all **Public IPs** to enforce a zero-trust routing architecture. Verified VNet Peering via the **Azure Serial Console** and internal Private IP pings (`10.20.x.x` to `10.30.x.x`).
*   **Quota & Cost Optimization:** Managed a strict **4-vCPU regional limit** (`norwayeast`) using `Standard_B2ats_v2` SKUs. ARM templates enforce `Delete NIC and Disk with VM` to prevent orphaned resource costs.
*   **Identity-Forward Configuration:** Enabled **System-Assigned Managed Identities** and **Trusted Launch (vTPM/Secure Boot)** on all nodes to meet future **SC-200/300** compliance requirements.

## 📁 Module 08: VNet Peering (Global)
*Connect two Azure Virtual Networks using global virtual network peering.*

### **Architecture Overview**
*   **VNet 1 (CoreServicesVnet):** `10.20.0.0/16` | Subnet: `DatabaseSubnet` (`10.20.20.0/24`)
*   **VNet 2 (ManufacturingVnet):** `10.30.0.0/16` | Subnet: `ManufacturingSystemSubnet` (`10.30.20.0/24`)
*   **Peering Status:** `Connected` (Bi-directional)

### **Verification Artifacts**
*   **Template:** `Module-08/azuredeploy.json` (Sanitized ARM Template)
*   **Connectivity Test:** ICMP Reply from `10.20.20.4` to `10.30.20.4` via Microsoft Backbone.

---
*Note: All private keys (.pem) are stored locally and excluded from this repository via .gitignore.*
