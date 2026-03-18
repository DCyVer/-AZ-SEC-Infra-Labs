# Unit 08: Zero-Trust Monitoring & Private Link Operations 🛡️
**Status:** 🟢 Verified | **Module:** M08 | **Date:** 2026-03-16

## 🏗️ Project Architecture
Deployment of a secure telemetry pipeline for a Zero-Internet 3-node Ubuntu cluster. Ingestion is achieved via Azure Private Link (AMPLS) and Data Collection Endpoints (DCE) to eliminate all public outbound exposure.

## 🛠️ Customization Choices
- **Compute Pivot:** Used Ubuntu 24.04 (B2ats_v2) and a Spot Instance (D2s_v3) to bypass a 4-vCPU trial quota while running a 6-vCPU cluster.
- **Hardening:** Utilized JIT NSG hole-punching (AzureUpdateDelivery) for dependency resolution, then returned to a Zero-Outbound state.
- **DNS Hijacking:** Manually mapped the norwayeast-1.handler.control (10.1.0.15) and .ingest (10.1.0.11) endpoints to bypass Private Link automation failures.

## 🚀 Proof of Work (Final Audit)
# 1. Verification of BOTH Private Link Handshakes
nslookup [DCE-ID].norwayeast.ingest.monitor.azure.com
# Result: 10.1.0.11 (Data Pipe)

nslookup [DCE-ID].norwayeast-1.handler.control.monitor.azure.com
# Result: 10.1.0.15 (Control Pipe - REQUIRED for config download)

# 2. Agent Process (The Heart)
ps -ef | grep mdsd
# Result: /opt/microsoft/azuremonitoragent/bin/mdsd -A -R ... (Active PID 4676)

# 3. KQL Ingestion (The Proof)
Heartbeat | summarize LastCall = max(TimeGenerated) by Computer
# Result: VM1-1, VM1-2, VM1-3 | 2026-03-16 02:10 AM UTC

# 4. Load Balancer Round-Robin Verification
for i in {1..6}; do curl -s http://10.1.0.10 | grep "Hello from"; done
# Result: VM1-1, VM1-2, VM1-3, VM1-1... (Symmetrical Distribution Confirmed)

# 5. Load Balancer Telemetry (The Bridge)
# Verification of Backend Health via AzureMetrics (Task 11/12)
AzureMetrics 

| where ResourceProvider == "MICROSOFT.NETWORK" and ResourceId contains "MYINTLOADBALANCER" 
| where MetricName == "DipAvailability" 
| summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 5m), ResourceId
# Result: 100% Availability confirmed across all 3 backend nodes (10.1.0.16-18).

## 📜 The War Log (Lessons & Conclusions)
- **The "Phantom" Success:** Azure reports "Succeeded" even if OS-level install fails. Verified via: ls /opt/microsoft/azuremonitoragent/bin/mdsd.
- **DNS Hierarchy Conflict:** Consolidating regional subdomains into a parent zone (norwayeast.monitor.azure.com) is mandatory for regional handler resolution.
- **Control Plane Hijack:** Confirmed that Private Link automation ignores regional handler endpoints. Manual DNS records for the .handler.control subdomain are mandatory for "Dark" VNet agent check-in.
- **Implicit Dependency Block:** Identified that the AMA installer (install.sh) requires Python 3 and OpenSSL. In a Zero-Outbound VNet, these must be temporarily permitted via Service Tags or pre-baked into the image to avoid "Phantom Success" where the extension exists but the binary (/opt/microsoft/...) is missing.
- **Probing the Dark:** Confirmed that in a "Dark" VNet, the Azure Load Balancer Health Probe (168.63.129.16) is often the first casualty of aggressive NSG hardening. Explicit Inbound 'Allow' for the AzureLoadBalancer Service Tag is mandatory to move the Insights Map from "Red/Unknown" to "Green/Healthy."
- **Latency vs. Reality:** Observed a ~15-minute ingestion lag between the LB "DipAvailability" metric and the Log Analytics AzureMetrics table. Real-time troubleshooting must rely on the 'Insights' blade, while long-term auditing uses KQL.
- **Spot Eviction Monitoring:** Leveraging the 'Resource Health' (Task 12) history allowed for the distinction between a network partition and a VM1-3 (Spot) de-allocation.

--

# 🛡️ Azure Security Infrastructure Labs (AZ-SEC)
**Comprehensive Implementation of Enterprise-Grade Networking & Security Controls**

## 🏗️ Documentation Framework
- Project Architecture: Technical summary and visual topology.
- Customization Choices: Documentation of pivots (Ubuntu 24.04/Spot) to reflect production engineering.
- Implementation Testing: Validation of "Dark" VNet telemetry (Zero Public Internet).
- Proof of Work: Direct evidence via CLI and KQL Heartbeats.
- Lessons & Conclusions (The War Log): Record of real-world platform bugs (DNS/Dependency).

## 🗺️ Project Navigation
- [M01-M07]: (Previous Labs Verified)
- [M08: Zero-Trust Monitoring](./M08-Zero-Trust-Monitoring/README.md) 🟢 - AMPLS, DCE, and Dark-VNet Telemetry.

---

# Unit 08: Zero-Trust Monitoring & Private Link Operations 🛡️
**Status:** 🟢 Verified | **Module:** M08 | **Date:** 2026-03-15

## 🏗️ Project Architecture
Deployment of a secure telemetry pipeline for a Zero-Internet 3-node Ubuntu cluster. Ingestion is achieved via Azure Private Link (AMPLS) and Data Collection Endpoints (DCE) to eliminate all public outbound exposure.

## 🛠️ Customization Choices
- Compute Pivot: Used Ubuntu 24.04 (B2ats_v2) and a Spot Instance (D2s_v3) to bypass a 4-vCPU trial quota while running a 6-vCPU cluster.
- Hardening: Utilized JIT NSG hole-punching (AzureUpdateDelivery) for dependency resolution, then returned to a Zero-Outbound state.
- DNS Hijacking: Manually mapped the norwayeast-1.handler.control (10.1.0.15) and .ingest (10.1.0.11) endpoints to bypass Private Link automation failures.

## 🚀 Proof of Work (Final Audit)
# Verification of BOTH Private Link Handshakes
nslookup [DCE-ID].norwayeast.ingest.monitor.azure.com
# Result: 10.1.0.11 (Data Pipe)

nslookup [DCE-ID].norwayeast-1.handler.control.monitor.azure.com
# Result: 10.1.0.15 (Control Pipe - REQUIRED for config download)

# Evidence of Heartbeat schema birth after cold-start buffer
Heartbeat | summarize count() by Computer
# Result: 3 nodes reporting (Verified @ 10:10 PM UTC)

# 2. Agent Process (The Heart)
ps -ef | grep mdsd
# Result: /opt/microsoft/azuremonitoragent/bin/mdsd -A -R ... (Active PID 4676)

# 3. KQL Ingestion (The Proof)
Heartbeat | summarize LastCall = max(TimeGenerated) by Computer
# Result: VM1-1, VM1-2, VM1-3 | 2026-03-15 10:10 PM UTC

## 📜 The War Log (Lessons & Conclusions)
- The "Phantom" Success: Azure reports "Succeeded" even if OS-level install fails. Verified via: ls /opt/microsoft/azuremonitoragent/bin/mdsd.
- DNS Hierarchy Conflict: Consolidating regional subdomains into a parent zone (norwayeast.monitor.azure.com) is mandatory for regional handler resolution.
- Log Verification: Ingestion status confirmed via local agent logs: /var/opt/microsoft/azuremonitoragent/log/mdsd.info.

## 📜 The War Log (Critical Additions)
- Control Plane Hijack: Confirmed that Private Link automation ignores regional handler endpoints. Manual DNS records for the .handler.control subdomain are mandatory for "Dark" VNet agent check-in.
- Implicit Dependency Block: Identified that the AMA installer (install.sh) requires Python 3 and OpenSSL. In a Zero-Outbound VNet, these must be temporarily permitted via Service Tags or pre-baked into the image to avoid "Phantom Success" where the extension exists but the binary (/opt/microsoft/...) is missing.


---
Maintainer: Dimitri Veraar (@DCyVer) | 8yr Dell Tech | Amsterdam SecOps

# 4. Load Balancer Telemetry (The Bridge)
# Verification of Backend Health via AzureMetrics (Task 11/12)
AzureMetrics 

| where ResourceProvider == "MICROSOFT.NETWORK" and ResourceId contains "MYINTLOADBALANCER"
| where MetricName == "DipAvailability" 
| summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 5m), ResourceId
# Result: 100% Availability confirmed across all 3 backend nodes (10.1.0.16-18).

# 5. Functional Dependency (Visual Validation)
# Insights Tab -> Map (Task 10)
# Result: Captured active flow distribution from Frontend (10.1.0.10) to Dark-Backend pool.

