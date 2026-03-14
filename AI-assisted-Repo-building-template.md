# AI-Assisted-Repo-Building-Template (V24.11.2)
**Date:** March 14, 2026  
**Status:** Protocol V24.11.2 Locked (Portable Sync)

---

*Note: AI is utilized as a SecOps Peer to automate the structural integrity of these repositories. All technical proofs, configurations, and architectural implementations were executed and recorded by the author in Norway East.*

---

#### **1. Project Governance & Intent**
This document defines the standards for technical consistency and evidence collection for the `AZ-SEC-Infra-Labs` repository. It ensures that all lab deployments align with the **AZ-700/SC-200** frameworks and maintain a professional, **Analyst-First** reporting standard.

#### **2. Structural Standards**
*   **Directory Naming:** `M[Number]-[Topic-Name]` (e.g., `M01-Virtual-Networking`).
*   **Portable Module Mandate:** All modules must be **Self-Contained**. All proofs (JSON/PNG/PS1) must reside within the specific module folder. The use of a centralized `Assets/` folder is deprecated to prevent cross-directory link rot.
*   **Tone:** "Analyst-First." Concise, objective, and cynical regarding legacy liabilities (Basic SKUs).

#### **3. Revision Standards (2026-Ready)**
*   **SKU Hard-Stop:** Only **Standard V2** or **AZ-family** SKUs (e.g., `VpnGw1`, `AppGwV2`) are permitted. Basic SKUs are documented as "Legacy Liabilities" due to the 2025/2026 retirement dates.
*   **Compliance Mapping:** **BIO2 v1.3** and **NIS2** compliance mapping is mandatory for all new architectural designs.
*   **Gateway Subnets:** Mandatory **/27 or larger** prefix for hybrid co-existence.

#### **4. Module README Hierarchy**
1.  **Technical Objective:** Precise problem statement (e.g., "Implement multi-region failover").
2.  **Implementation Checklist:** Chronological list of Azure resources deployed.
3.  **Local Resource Mapping:** Evidence linked using **Local Relative Pathing** (e.g., `./M01-U04-Topology.png`). Global or absolute paths are prohibited.
4.  **Security Validation (The Sober Proof):** Direct CLI/Header evidence of success (e.g., `curl -I`, `nslookup`).
5.  **Analyst Perspective (BIO2/NIS2):** 2-sentence summary mapping the architecture to a risk-based compliance outcome.
