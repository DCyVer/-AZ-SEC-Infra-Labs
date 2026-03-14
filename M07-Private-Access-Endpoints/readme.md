# Unit [U05]: PaaS Access via Service Endpoints 🛡️
**Status:** 🟢 Verified | **Module:** M07 | **Date:** 2026-03-14

## 🏗️ Project Architecture
Hardened an Azure Storage Account by Enforcement of a "Secret Tunnel" (Service Endpoint) for VNet-internal traffic while dropping the "Iron Curtain" on the public internet.

![Topology](./05-Topology.png)
*Figure 1: CoreServicesVNet architecture with isolated Private Subnet.*

## 🛠️ Customization Choices
*   **Dual-OS Pivot:** Deployed **Ubuntu 24.04** and **Windows Server 2022** (Spot) to validate cross-platform parity.
*   **Incident Response:** Performed an emergency **Key Rotation** (regenerated access keys) after credentials were leaked in console logs to maintain environment integrity.

## 🎯 Implementation Testing
*   **Phase 1 (Baseline):** Verified the initial path from **UbuntuVM (10.20.0.4)** to the vault via `nc`.
    ![Ubuntu Baseline](./01-Ubuntu-SSH-preliminary-test-pass.png)
*   **Phase 2 (Infrastructure):** Enabled the **Storage Service Endpoint** on the Subnet and locked the **Storage Firewall** to "Selected Networks."
    ![Network Settings](./03-Storage-Firewall-Selected-Networks.png)
*   **Phase 3 (Remediation):** Rotated the compromised Storage Account Key and purged the exposed credentials.
    ![Security Audit](./04-Storage-key-purged.png)

## 🚀 Proof of Work
Verified authorized internal tunnel access while simultaneously confirming public internet lockout.

![Final Verification](./06-Ubuntu-Win-VM-Access-localPC-denied.png)
*Figure 2: WinScout Success vs. Local PC Access Denied (Error 5).*
