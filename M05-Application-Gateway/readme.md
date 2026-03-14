# 🌐 Module 05: Application Gateway & Front Door
**Implementation: Layer 7 Regional Traffic Orchestration & Global Acceleration**

## 🏗️ Project Architecture
Implementation of regional Layer 7 application-aware routing and SSL termination for the vnet-spoke-no-01 Web-Tier.

*   **Regional L7:** Azure Application Gateway (WAF v2) fronting B2ats_v2 Ubuntu nodes in Norway East.
*   **Global L7:** Architectural evaluation of Azure Front Door for Anycast edge acceleration (Provisioning suspended per Subscription constraints).

## ⚖️ Customization Rationale
*   **WAF v2 Pivot:** Deployed WAF v2 to enforce OWASP Top 10 protection at the edge. 
*   **Dedicated /24 Subnet:** Provisioned a dedicated /24 prefix. While /26 is the technical minimum, a /24 is the MS Learn standard for v2 SKUs to ensure address space for autoscaling and platform upgrades.
*   **Ubuntu Workflow:** Standardized on Ubuntu 24.04 backends to validate X-Forwarded-For header injection and ensure backend identity preservation through the proxy.

## 🧪 Implementation Testing
1.  **Path-Based Routing:** Verified traffic distribution logic for /images/* and /video/* backend pools.
2.  **SSL Offloading:** Confirmed SSL termination at the Gateway, reducing crypto-processing overhead on B-Series backend VMs.
3.  **WAF 'Prevention' Mode:** Validated drop-actions for SQL injection and XSS patterns, confirmed via ApplicationGatewayFirewallLog.

## 🔍 Proof of Work (Technical Evidence)
- **Topology Diagram:** [M05-AppGW-Diagram.png](../Assets/M05-AppGW-Diagram.png) 🖼️
- **WAF Policy Export:** [M05-WAF-Rules.json](../Assets/M05-WAF-Rules.json) 📄
- **Header Verification:** curl -I http://<AppGW_Public_IP>/ (Expected: Server: Microsoft-HTTPAPI/2.0)

## 🧠 Lessons & Conclusions (The "War Log")
*   **Quota Bottleneck:** Unit M05U06 (Front Door) deployment is suspended due to Subscription-level entitlement constraints (Student/Trial Tiers). Ref: MS Q&A 1729771. Documented as an external provider-side limitation.
*   **NSG "Ghost Spaces":** AppGW v2 requires inbound traffic on TCP ports 65200-65535 for the Gateway Manager service tag. Missing these rules in the subnet NSG triggers an immediate Unhealthy status regardless of backend VM health.
*   **L4 vs L7 Latency:** Documented a measurable increase in TTFB compared to M04 (Load Balancer), justified by mandatory WAF inspection and cookie-based session affinity requirements.
