# AI-Assisted-Repo-Building-Template (V2.0)
**Date:** March 9, 2026  
**Status:** Protocol V15.12 Locked  

---

*Note: AI is utilized solely to automate the consistent maintenance and structural integrity of these repositories. All technical proofs, configurations, and architectural implementations were executed and recorded by the author. Images and screen captures are authentic representations of live environments created by the author, unless explicitly annotated, cropped, magnified, or specifically mentioned.*

---

#### **1. Project Governance & Intent**
This document defines the standards for technical consistency and evidence collection for the `AZ-SEC-Infra-Labs` repository. It ensures that all lab deployments align with the **AZ-700/SC-200** frameworks and maintain a professional, evidence-first reporting standard.

#### **2. Structural Standards**
To maintain a high-signal portfolio, every module added must adhere to the following:
*   **Directory Naming:** `[Module-Number]-[Topic-Name]` (e.g., `06-Name-Resolution`).
*   **Tone:** "Analyst-First." Concise, objective, and devoid of marketing superlatives.
*   **The Bridge Logic:** Every lab must explicitly state how the networking configuration (AZ-700) enables a security outcome (SC-200).
*   **Legacy Preservation:** Technical proofs and configurations recorded prior to **March 9, 2026**, are preserved as authentic historical records. Reverse-compliance is not required for these existing assets.

#### **3. Revision Standards (Effective March 9, 2026)**
All implementation and documentation from this date forward must adhere to the following architectural shifts. These replace legacy standards to remain "2026-Ready" for Amsterdam In-House SecOps requirements:
*   **Regulatory Pivot:** **BIO2 v1.3 (Risk-Based)** and **ISO 27001:2023** replace the legacy BBN-fixed levels and BIO 1.04.
*   **Gateway Architecture:** **AZ-family SKUs** (e.g., `VpnGw1AZ`, `ErGwScale`) replace deprecated *Standard* and *High Performance* SKUs.
*   **Outbound Logic:** **Explicit Outbound Access** (via NAT Gateway or Azure Firewall) replaces "Implicit/Default Outbound Access" (reflecting the March 31, 2026 API shift).

#### **4. Module README Template**
Each sub-directory must contain a `README.md` following this exact hierarchy:
1.  **Technical Objective:** Precise problem statement (e.g., "Implement split-horizon DNS to prevent internal IP exposure").
2.  **Implementation Checklist:** Chronological list of Azure resources deployed.
3.  **Security Validation (The Evidence):**
    *   **Connectivity Proof:** CLI output (e.g., `ping` or `Test-NetConnection`).
    *   **Resolution Proof:** DNS resolution output (e.g., `nslookup` or `dig`).
    *   **Routing/Policy Proof:** Screenshot of "Effective Routes" or NSG rules confirming traffic flow control.
4.  **Analyst Perspective:** A 2-sentence summary on the risk mitigated, specifically mapping the architecture to **BIO2 v1.3** or **ISO 27001:2023** for all post-revision labs.

#### **5. AI Orchestration Rules**
When generating content for this repository, the AI partner must:
*   **Verify Accuracy:** Cross-reference all technical terms with current Microsoft documentation.
*   **Legacy Awareness:** Respect pre-existing lab configurations while flagging deprecated SKUs for any *new* design suggestions.
*   **Maintain Integrity:** Adhere to **Protocol V15.11 (Integrity Guardrail)**—no structural omissions or data pruning allowed during roadmap or list generation.
*   **Admit Flaws:** In the event of a technical or tone-based error, acknowledge the correction immediately without defensive framing.
