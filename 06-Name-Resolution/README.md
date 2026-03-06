# 06: Designing and Implementing Name Resolution

### **Technical Objective**
Establish reliable, private FQDN resolution within a virtual network environment to prevent internal infrastructure exposure to the public internet and ensure seamless service connectivity.

### **Implementation Checklist**
- [x] Deployment of Azure Private DNS Zone (`contoso.com`).
- [x] Virtual Network Link configuration between `CoreServicesVnet` and the Private DNS Zone.
- [x] Manual/Autoregistration of internal host A-records.
- [x] Verification of split-horizon DNS functionality.

### **Security Validation (The Evidence)**

#### **1. Resolution Proof (nslookup)**
*Verification of the DNS resolver returning the internal Private IP instead of a public endpoint.*
![DNS Resolution Proof](./assets/01-nslookup-validation.png)

#### **2. Infrastructure Configuration**
*Confirmation of the Private DNS Zone linked status to the target VNet.*
![DNS Zone Link](./assets/02-private-dns-link.png)

### **Analyst Perspective**
By implementing Private DNS Zones, we eliminate the need for host-file manipulation and reduce the attack surface by ensuring internal resource names are only resolvable within authorized network segments. This configuration is a prerequisite for mitigating DNS-based exfiltration and lateral movement.
