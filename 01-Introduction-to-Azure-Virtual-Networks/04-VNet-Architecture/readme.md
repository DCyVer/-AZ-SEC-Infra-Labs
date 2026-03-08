# 04: Designing and Implementing Virtual Networks

### **Technical Objective**
Establish a globally distributed Hub-and-Spoke network foundation using Infrastructure-as-Code (IaC). This architecture provides isolated segments for sensitive workloads across multiple geographic regions while maintaining a centralized administrative boundary.

### **Reference Curriculum**
*   [Microsoft Learn: M01-U4 Exercise](https://learn.microsoft.com/en-us/training/modules/introduction-to-azure-virtual-networks/4-exercise-design-implement-virtual-network-azure)
*   [Official Lab Instructions (GitHub)](https://microsoftlearning.github.io/AZ-700-Designing-and-Implementing-Microsoft-Azure-Networking-Solutions/Instructions/Exercises/M01-Unit%204%20Design%20and%20implement%20a%20Virtual%20Network%20in%20Azure.html)

### **Implementation Checklist**
- [x] **CoreServicesVnet (Hub):** Deployed in `East US` with 4 tier-segmented subnets.
- [x] **ManufacturingVnet (Spoke 1):** Deployed in `West Europe` for regional industrial workloads.
- [x] **ResearchVnet (Spoke 2):** Deployed in `Southeast Asia` for experimental data isolation.
- [x] **IaC Validation:** All resources deployed via signed ARM templates to ensure environmental consistency.

### **Security Validation (The Evidence)**

#### **1. Global Infrastructure Topology**
![Resource Group Topology](./assets/rg-global-topology.png)

#### **2. Hub Subnet Segmentation**
![Hub Overview](./assets/hub-vnet-overview.png)

#### **3. Regional Spoke Validation**
![Manufacturing Overview](./assets/mfg-vnet-overview.png)

---

### **Infrastructure-as-Code (IaC)**
The blueprints used to deploy this environment are located in the [`/templates`](./templates/) directory:
*   [`CoreServicesVnet.json`](./templates/CoreServicesVnet.json)
*   [`ManufacturingVnet.json`](./templates/ManufacturingVnet.json)
*   [`ResearchVnet.json`](./templates/ResearchVnet.json)

---

### **Analyst Perspective**
This multi-region tiered architecture enforces **Network Segmentation** at the transport layer, effectively reducing the blast radius of a potential web-tier compromise by isolating the database and manufacturing sensor tiers.
