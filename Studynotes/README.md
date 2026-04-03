# 🛡️ Azure Security Infrastructure Labs (AZ-SEC)
**Comprehensive Implementation of Enterprise-Grade Networking & Security Controls**

## ⚖️ Engineering Methodology
Each lab is documented using a standardized framework focused on architectural integrity and cost-optimization for a career-pivot showcase.

### 🏗️ Documentation Framework:
- **Project Architecture:** Technical summary and visual topology.
- **Customization Choices:** Documentation of pivots from lab defaults (e.g., B2ats_v2 Ubuntu/Standard SKUs) to reflect production-grade engineering.
- **Implementation Testing:** Description of validation phases and security scenarios.
- **Proof of Work:** Direct evidence via CLI outputs and response headers.
- **Lessons & Conclusions (The "War Log"):** Record of real-world friction, platform bugs, and key architectural takeaways.

## 📁 Repository Structure
- **M[01-06] Modular Folders/**: Self-contained implementation handbooks.
  - **README.md**: Detailed Module/Unit documentation.
  - **[Local Proof]**: Relative-pathed JSON templates, PNG topologies, and CLI outputs.
- **README.md**: Executive Dashboard and global project navigation.

## 🗺️ Project Navigation
- [M01: Virtual Networking](./M01-Virtual-Networking/README.md) 🟢 - Foundational Segmentation & DNS.
- [M02: Hybrid Networking](./M02-Hybrid-Networking/README.md) 🟢 - VPN Redundancy & vWAN Transit.
- [M03: ExpressRoute](./M03-ExpressRoute/README.md) 🟢 - Private Backhaul & BGP Dynamics.
- [M04: Load Balancing](./M04-Load-Balancing/README.md) 🟢 - Regional L4 & Global DNS Failover.
- [M05: Application Gateway](./M05-Application-Gateway/README.md) 🟢 - Regional L7 & WAF Prevention.
- [M06: Network Security](./M06-Network-Security/README.md) 🟢 - FW Policies & LPM Routing Bypasses.

## ⚙️ Tech Stack & Requirements
- **Infrastructure:** ARM Templates (JSON), Azure CLI 2.x
- **Provisioning:** PowerShell (IIS & Workload Automation)
- **Environment:** Norway East (Primary) | Ubuntu 24.04 LTS (B2ats_v2) & Windows Server 2019 [Smalldisk]

## ⚖️ Global Environment Baseline
- **Security:** Default Private-IP only; restricted Public entry-points (Standard SKUs).
- **Performance:** Standard HDD utilized for trial quota stability; B-Series burstable compute.

---
**Disclaimer:** These labs are for architectural demonstration. Always validate against the Microsoft Cloud Security Benchmark before production use.

**Maintainer:** Dimitri Veraar (@DCyVer) | *8yr Dell Tech | Amsterdam SecOps*