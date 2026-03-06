*Note: AI is utilized solely to automate the consistent maintenance and structural integrity of these repositories. All technical proofs, configurations, and architectural implementations were executed and recorded by the author. Images and screen captures are authentic representations of live environments created by the author, unless explicitly annotated, cropped, magnified, or specifically mentioned.*

# AI-Assisted-Repo-Building-Template (V1.0)
**Date:** March 6, 2024  
**Status:** Protocol V13.0 Locked  

---

#### **1. Project Governance & Intent**
This document defines the standards for technical consistency and evidence collection for the `AZ-SEC-Infra-Labs` repository. It ensures that all lab deployments align with the **AZ-700/SC-200** frameworks and maintain a professional, evidence-first reporting standard.

#### **2. Structural Standards**
To maintain a high-signal portfolio, every module added must adhere to the following:
*   **Directory Naming:** `[Module-Number]-[Topic-Name]` (e.g., `06-Name-Resolution`).
*   **Tone:** "Analyst-First." Concise, objective, and devoid of marketing superlatives (no "mastery" or "expertise").
*   **The Bridge Logic:** Every lab must explicitly state how the networking configuration (AZ-700) enables a security outcome (SC-200).

#### **3. Module README Template**
Each sub-directory must contain a `README.md` following this exact hierarchy:
1.  **Technical Objective:** Precise problem statement (e.g., "Implement split-horizon DNS to prevent internal IP exposure").
2.  **Implementation Checklist:** Chronological list of Azure resources deployed.
3.  **Security Validation (The Evidence):**
    *   **Connectivity Proof:** CLI output (e.g., `ping` or `Test-NetConnection`).
    *   **Resolution Proof:** DNS resolution output (e.g., `nslookup` or `dig`).
    *   **Routing/Policy Proof:** Screenshot of "Effective Routes" or NSG rules confirming traffic flow control.
4.  **Analyst Perspective:** A 2-sentence summary on the risk mitigated by this specific architecture.

#### **4. AI Orchestration Rules**
When generating content for this repository, the AI partner must:
*   **Verify Accuracy:** Cross-reference all technical terms with current Microsoft Learn documentation.
*   **Maintain SEO:** Use industry-standard keywords (e.g., VNet Peering, Private DNS, Hub-and-Spoke).
*   **Admit Flaws:** In the event of a technical or tone-based error, acknowledge the correction immediately without defensive framing.
