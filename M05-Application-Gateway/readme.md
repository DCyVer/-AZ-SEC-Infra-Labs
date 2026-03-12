# Module 05: Application Gateway & Front Door
**Implementation: Layer 7 Load Balancing and Global Acceleration**

## 🏗️ Application Gateway (L7)
- **SKU:** WAF v2 (Standard + Web Application Firewall)
- **Frontend:** Public IP (Port 80/443)
- **Backend:** `vnet-spoke-no-01` Web-Tier (Ubuntu nodes)
- **Features:** Cookie-based affinity and SSL Termination.

## 📁 Technical Evidence
- **Topology:** [M05-AppGW-Diagram.png](../Assets/M05-AppGW-Diagram.png)
- **WAF Policy:** [M05-WAF-Rules.json](../Assets/M05-WAF-Rules.json)

## ⚖️ Implementation Details
1. **Routing Rules:** Path-based routing configured for `/images/*` and `/video/*` traffic distribution.
2. **Security:** WAF enabled in 'Prevention' mode to mitigate OWASP Top 10 vulnerabilities.

## 🛠️ Global Delivery Constraints (Front Door)
- **Unit M05U06:** Azure Front Door (Standard/Premium) implementation was evaluated.
- **Limitation:** Subscription-level entitlement constraints (Student/Trial Tiers) currently restrict the provisioning of Front Door resources (Ref: MS Q&A 1729771).
- **Outcome:** Unit is documented as architecturally understood but deployment is suspended due to provider-side quota restrictions.
