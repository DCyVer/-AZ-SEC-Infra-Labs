# AI-Assisted-Repo-Building-Template (V24.10.2)
**Date:** March 12, 2026  
**Status:** Protocol V24.10.2 Locked (Modular Alignment)

---

*Note: AI is utilized solely to automate the consistent maintenance and structural integrity of these repositories. All technical proofs, configurations, and architectural implementations were executed and recorded by the author. Images and screen captures are authentic representations of live environments created by the author, unless explicitly annotated, cropped, magnified, or specifically mentioned.*

---

#### **1. Project Governance & Intent**
This document defines the standards for technical consistency and evidence collection for the `AZ-SEC-Infra-Labs` repository. It ensures that all lab deployments align with the **AZ-700/SC-200** frameworks and maintain a professional, **Stateless Observer** reporting standard.

#### **2. Structural Standards**
To maintain a high-signal portfolio, every module added must adhere to the following:
*   **Directory Naming:** `M[Number]-[Topic-Name]` (e.g., `M01-Virtual-Networking`).
*   **Portable Module Mandate:** All modules must be **Self-Contained**. All proofs (JSON/PNG/PS1) must reside within the specific module folder. The use of a centralized `Assets/` folder is deprecated to prevent cross-directory link rot.
*   **Tone:** "Analyst-First." Concise, objective, and devoid of marketing superlatives.
*   **The Bridge Logic:** Every lab must explicitly state how the networking configuration (AZ-700) enables a security outcome (SC-200).

#### **3. Revision Standards (Effective March 12, 2026)**
All implementation and documentation from this date forward must adhere to the following architectural shifts to remain "2026-Ready" for Amsterdam SecOps:
*   **Regulatory Pivot:** **BIO2 v1.3 (Risk-Based)** and **NIS2** compliance mapping is mandatory for all new architectural designs.
*   **SKU Hard-Stop:** Only **Standard V2** or **AZ-family** SKUs (e.g., `VpnGw1AZ`, `AppGwV2`) are permitted. *Exception:* Standard SKUs are permitted where AZ-family quotas are restricted by Subscription Tier, provided the design logic remains v2-compliant.
*   **Layer 7 Compatibility:** All Load Balancing implementations must validate **Host-Header Handshaking** to prevent platform rejections.

#### **4. Module README Template**
Each sub-directory must contain a `README.md` following this exact hierarchy:
1.  **Technical Objective:** Precise problem statement (e.g., "Implement multi-region failover with HTTPS health probing").
2.  **Implementation Checklist:** Chronological list of Azure resources deployed.
3.  **Local Resource Mapping:** All assets must be linked using **Relative Pathing** (e.g., `[Topology](./M01-U04-Topology.png)`). Global or absolute paths are prohibited.
4.  **Security Validation (The Sober Proof):**
    *   **External Resolution:** DNS verification via `nslookup [URL] 8.8.8.8`.
    *   **Application Integrity:** Successful page load in a browser via the Global URL.
    *   **Routing/Policy Proof:** Screenshot of "Effective Routes" or NSG rules confirming traffic flow control.
5.  **Analyst Perspective:** A 2-sentence summary on the risk mitigated, specifically mapping the architecture to **BIO2 v1.3** or **NIS2**.

#### **5. AI Orchestration Rules**
When generating content for this repository, the AI partner must:
*   **Rule of Pixel-Truth:** Prohibited from describing UI elements or SKUs not visibly present in the author's uploaded screenshots.
*   **Binary Integrity:** If a screenshot shows a SKU mismatch or Quota error, the AI must trigger a **HALT** state rather than suggesting "creative" workarounds.
*   **Zero-Apology Reset:** If a structural drift occurs, the AI must recenter on the verified technical data immediately without meta-commentary.
