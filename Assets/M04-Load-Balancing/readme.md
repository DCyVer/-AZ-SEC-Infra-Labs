# Module 04: Load Balancing (L4)
**Implementation: Azure Standard Load Balancer**

## 🏗️ Architecture
- **Type:** Public Standard Load Balancer
- **SKU:** Standard (Required for HA Port support and Private Link)
- **Frontend IP:** `pip-slb-frontend-no-01`
- **Backend Pool:** `be-pool-web-01` (Ubuntu 24.04 nodes)

## 📁 Technical Evidence
- **Topology:** [M04-SLB-Diagram.png](../Assets/M04-SLB-Diagram.png)
- **JSON Export:** [M04-SLB-Config.json](../Assets/M04-SLB-Config.json)

## ⚖️ Implementation Details
1. **Health Probes:** Configured for TCP 80/443 with a 5-second interval.
2. **Load Balancing Rules:** 
   - Rule 01: Port 80 (HTTP) -> Port 80 (Backend)
   - Rule 02: Port 443 (HTTPS) -> Port 443 (Backend)
3. **High Availability:** Distributed across Availability Zones where supported by the Region (Norway East).

## 🛠️ Configuration Notes
- **Persistence:** Client IP (2-tuple) session persistence enabled for stateful application testing.
- **Outbound Rules:** Explicit Outbound NAT rules configured to manage backend internet egress.
