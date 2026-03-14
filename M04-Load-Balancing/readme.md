# ⚖️ Module 04: Load Balancing (Non-HTTP/S)
**Implementation: Regional Layer 4 High-Availability & Global DNS Orchestration**

## 🏗️ Unit 04: Regional Standard Load Balancer (SLB)
Implementation of regional Layer 4 traffic distribution for non-web workloads fronting the vnet-spoke-no-01 backend pool.

*   **Logic:** Hash-based distribution (5-tuple) for TCP/UDP traffic.
*   **SKU Pivot:** Standard Load Balancer utilized over the legacy Basic SKU to enable High-Availability (HA) Ports.
*   **Backend:** B2ats_v2 Ubuntu nodes in Norway East configured for "Secure by Default" traffic flow.

### ⚖️ SLB Customization Rationale
*   **Standard SKU Mandate:** Selected Standard over Basic to support HA-Ports and Diagnostic Settings. Basic SKUs are officially retiring in September 2025 and lack integrated security postures.
*   **HA-Ports Feature:** Enabled "All-Port" balancing to eliminate the administrative bottleneck of per-port rule sets, allowing full high-availability for all backend services.
*   **B2ats_v2 Optimization:** Standardized backend compute on B-Series Ubuntu to maintain performance consistency across the regional infrastructure.

### 🧪 SLB Implementation Testing
1.  **Flow Hash Verification:** Confirmed session persistence and traffic distribution across backend nodes using concurrent TCP streams.
2.  **Health Probe Resiliency:** Validated sub-10s failover by manually terminating the listener service on a primary node.

---

## 🏗️ Unit 06: Global Traffic Manager (GTM)
DNS-based global endpoint orchestration for multi-regional failover and latency-based routing.

*   **Logic:** DNS CNAME redirection based on endpoint health and routing priority.
*   **Routing Method:** "Priority" routing configured for primary (Norway East) and secondary failover targets.

### ⚖️ GTM Customization Rationale
*   **DNS-Level Steering:** Implemented Traffic Manager as the global entry point. Unlike AppGW (L7), Traffic Manager works at the DNS level, directing clients to endpoints without proxying the data.
*   **Health Probing Identity:** Configured custom health probes to monitor endpoint availability, ensuring traffic is only routed to responsive nodes.

### 🧪 GTM Implementation Testing
1.  **DNS Priority Logic:** Verified that traffic only shifts to the secondary region when the Norway East endpoint reports as degraded.
2.  **Failover Propagation:** Documented the inherent delay between endpoint failure and DNS cache expiration (controlled by TTL).

---

## 🧠 Lessons & Conclusions (The "War Log")
*   **Basic SKU Liability:** Basic Load Balancers lack "Secure by Default" posture and HA-Port support. They are documented here as a legacy constraint to be avoided in professional production.
*   **TTL Propagation Lag:** Traffic Manager failover is limited by DNS TTL. This creates a measurable "Propagation Delay" during outages that proxy-based L7 solutions do not suffer from.
*   **Frontend IP Dependency:** A Standard LB requires a Standard Public IP; mixing Basic/Standard tiers results in a hard deployment failure.
