# AI-Assisted-Repo-Building-Template (V22.5)
**Date:** March 10, 2026  
**Status:** Protocol V22.5 Locked (Stateless Observer Mode)

---

*Note: AI is utilized solely to automate the consistent maintenance and structural integrity of these repositories. All technical proofs, configurations, and architectural implementations were executed and recorded by the author. Images and screen captures are authentic representations of live environments created by the author, unless explicitly annotated, cropped, magnified, or specifically mentioned.*

---

#### **1. Project Governance & Intent**
This document defines the standards for technical consistency and evidence collection for the `AZ-SEC-Infra-Labs` repository. It ensures that all lab deployments align with the **AZ-700/SC-200** frameworks and maintain a professional, **Stateless Observer** reporting standard.

#### **2. Structural Standards**
To maintain a high-signal portfolio, every module added must adhere to the following:
*   **Directory Naming:** `[Module-Number]-[Topic-Name]` (e.g., `04-Load-Balancing`).
*   **Tone:** "Analyst-First." Concise, objective, and devoid of marketing superlatives.
*   **The Bridge Logic:** Every lab must explicitly state how the networking configuration (AZ-700) enables a security outcome (SC-200).
*   **Legacy Preservation:** Technical proofs and configurations recorded prior to **March 9, 2026**, are preserved as authentic historical records. 

#### **3. Revision Standards (Effective March 10, 2026)**
All implementation and documentation from this date forward must adhere to the following architectural shifts to remain "2026-Ready" for Amsterdam SecOps:
*   **Regulatory Pivot:** **BIO2 v1.3 (Risk-Based)** and **NIS2** compliance mapping is mandatory for all new architectural designs.
*   **SKU Hard-Stop:** Only **Standard V2** or **AZ-family** SKUs (e.g., `VpnGw1AZ`, `AppGwV2`) are permitted, reflecting the April 2026 V1 retirements.
*   **Layer 7 Compatibility:** All Load Balancing implementations must validate **Host-Header Handshaking** to prevent `400 InvalidUri` platform rejections.

#### **4. Module README Template**
Each sub-directory must contain a `README.md` following this exact hierarchy:
1.  **Technical Objective:** Precise problem statement (e.g., "Implement multi-region failover with HTTPS health probing").
2.  **Implementation Checklist:** Chronological list of Azure resources deployed.
3.  **Security Validation (The Sober Proof):**
    *   **External Resolution:** DNS verification via `nslookup [URL] 8.8.8.8` to bypass recursive caching.
    *   **Application Integrity:** Successful page load in a browser via the **Global URL** (verified via high-contrast custom content).
    *   **Routing/Policy Proof:** Screenshot of "Effective Routes" or NSG rules confirming traffic flow control.
4.  **Analyst Perspective:** A 2-sentence summary on the risk mitigated, specifically mapping the architecture to **BIO2 v1.3** or **NIS2**.

#### **5. AI Orchestration Rules**
When generating content for this repository, the AI partner must:
*   **Rule of Pixel-Truth:** Prohibited from describing UI elements, buttons, or SKUs not visibly present in the author's uploaded screenshots.
*   **Binary Integrity:** If a screenshot shows a SKU mismatch or Quota error, the AI must trigger a **HALT** state rather than suggesting "creative" workarounds.
*   **Zero-Apology Reset:** If a structural drift occurs, the AI must recenter on the verified technical data immediately without meta-commentary.
*   **Least-Privilege Search:** Explicit authorization is required for any external web-query to verify 2026 lifecycle data.
