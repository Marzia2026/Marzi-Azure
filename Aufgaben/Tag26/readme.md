
# Microsoft Azure Hybrid Cloud – Individual Learning Phase (ILP)

## Overview

This project demonstrates the analysis and design of a Hybrid Cloud solution using Microsoft Azure for a medium-sized manufacturing company.

---

# Task 1 – Compare Cloud Models

| Criteria | Private Cloud | Public Cloud | Hybrid Cloud |
|----------|---------------|--------------|--------------|
| Resource Location | Company Data Center | Microsoft Azure | On-Premises + Azure |
| Management | Company IT | Microsoft | Shared Responsibility |
| Scalability | Limited by Hardware | Very High | Flexible |
| Security & Compliance | Full Control | Azure Security & Compliance | Sensitive data stays on-premises |
| Cost | High CAPEX | Pay-as-you-go | Balanced CAPEX & OPEX |
| Typical Use Cases | Banking, Healthcare | Web Apps, Startups | Enterprise Cloud Migration |

### Practical Examples

| Cloud Model | Example |
|-------------|---------|
| **Private Cloud** | A bank hosts customer databases in its own data center to meet strict compliance requirements. |
| **Public Cloud** | A software startup deploys its applications entirely on Azure to benefit from automatic scaling. |
| **Hybrid Cloud** | A manufacturing company keeps its ERP system on-premises while using Azure Backup, Azure Monitor, and Microsoft Entra ID. |

---

# Task 2 – Hybrid Business Scenario Analysis

## Why Hybrid Cloud?

| Reason | Technical Perspective |
|---------|-----------------------|
| ERP system cannot move to Azure yet | Migration |
| Secure access for remote offices | Operations |
| High availability requirements | Availability |
| Compliance and sensitive business data | Security |
| Gradual cloud adoption | Cost |

## Azure Connection Requirements

| Requirement | Description |
|-------------|-------------|
| Secure Connectivity | Encrypted communication between Azure and the local data center |
| Identity Integration | Synchronize Active Directory with Microsoft Entra ID |
| Backup & Disaster Recovery | Protect critical business systems and data |

---

# Task 3 – On-Premises to Azure Connections

| Requirement | Connection | Azure Service | Purpose |
|-------------|------------|---------------|---------|
| Network | Site-to-Site VPN | Azure VPN Gateway | Secure communication |
| Identity | Directory Sync | Microsoft Entra ID Connect | Single Sign-On & Identity Synchronization |
| Files | File Synchronization | Azure File Sync | Hybrid file storage |
| Monitoring | Hybrid Management | Azure Arc + Azure Monitor | Central monitoring |
| Backup | Cloud Backup | Azure Backup | Data protection |
| Disaster Recovery | VM Replication | Azure Site Recovery | Business continuity |

---

# Task 4 – Hybrid Azure Services

| Azure Service | Description | Benefit | Scenario Component | Prerequisites |
|---------------|-------------|----------|--------------------|---------------|
| Azure Arc | Manage on-prem resources from Azure | Centralized management | Windows/Linux Servers | Azure Subscription |
| Microsoft Entra ID | Identity management | Single Sign-On | Active Directory | Entra Connect |
| Azure VPN Gateway | Secure hybrid networking | Encrypted connection | Network | VPN Device |
| Azure Backup | Cloud backup | Data protection | File Server & VMs | Recovery Services Vault |
| Azure Site Recovery | Disaster Recovery | Failover capability | ERP & VMs | Azure Recovery Services |
| Azure File Sync | Synchronize files | Shared storage | File Server | Storage Account |
| Azure Monitor | Monitor infrastructure | Alerts & Performance | Entire environment | Azure Subscription |

## Most Important Services

| Service | Reason |
|----------|--------|
| Azure VPN Gateway | Provides secure hybrid connectivity |
| Microsoft Entra ID | Centralized authentication and access control |
| Azure Backup | Protects business-critical data |

---

# Task 5 – Hybrid Target Architecture

```text
                    Microsoft Azure
+------------------------------------------------+
| Microsoft Entra ID                             |
| Azure VPN Gateway                              |
| Azure Backup                                   |
| Azure Site Recovery                            |
| Azure Monitor                                  |
| Azure File Sync                                |
| Azure Arc                                      |
+----------------------+-------------------------+
                       |
               Site-to-Site VPN
                       |
====================================================
             On-Premises Data Center

 Active Directory
 ERP System
 Windows Servers
 Linux Servers
 File Server

             Remote Branch Offices
```

## Why is this Architecture Hybrid?

- Critical business applications remain on-premises.
- Azure extends the local infrastructure with cloud services.
- Identity, monitoring, backup, and disaster recovery are managed through Azure.

### Systems Remaining On-Premises

- ERP System
- Active Directory
- Windows Servers
- Linux Servers
- File Server

### Azure Adds

- Secure VPN Connectivity
- Identity Synchronization
- Cloud Backup
- Disaster Recovery
- Monitoring
- File Synchronization

### Recommended Next Steps

1. Configure Azure VPN Gateway.
2. Synchronize Active Directory with Microsoft Entra ID.
3. Deploy Azure Backup and Azure Site Recovery.

---

# Extension Task 1 – Service Comparison

## Site-to-Site VPN vs ExpressRoute

| Feature | Site-to-Site VPN | ExpressRoute |
|----------|------------------|--------------|
| Purpose | Secure Internet VPN | Dedicated Private Connection |
| Advantages | Low Cost, Easy Deployment | High Performance, Low Latency |
| Limitations | Internet Dependency | Higher Cost |
| Best For | SMBs | Large Enterprises |

## Azure Backup vs Azure Site Recovery

| Feature | Azure Backup | Azure Site Recovery |
|----------|--------------|---------------------|
| Purpose | Data Backup | Disaster Recovery |
| Advantage | Restore files and VMs | Automatic Failover |
| Limitation | No failover | More complex configuration |
| Best For | Daily backup | Business continuity |

---

# Extension Task 2 – Risks

| Risk | Countermeasure |
|------|----------------|
| Network latency | Use ExpressRoute or optimize VPN |
| Identity conflicts | Deploy Microsoft Entra ID Connect |
| Security vulnerabilities | Enable MFA and Zero Trust |
| Cost overruns | Use Azure Cost Management |
| Backup failures | Test backup and recovery regularly |
| Management complexity | Use Azure Arc and Azure Monitor |

---

# Extension Task 3 – Management Summary

A Hybrid Cloud solution enables the company to modernize its IT infrastructure without replacing existing critical systems. The ERP system remains on-premises, while Azure provides secure connectivity, identity management, monitoring, backup, and disaster recovery. This approach minimizes migration risks, improves business continuity, and enhances security. The recommended first step is establishing a Site-to-Site VPN and synchronizing Active Directory with Microsoft Entra ID.

---

## Technologies

- Microsoft Azure
- Microsoft Entra ID
- Azure VPN Gateway
- Azure Backup
- Azure Site Recovery
- Azure Arc
- Azure File Sync
- Azure Monitor

---

## References

- Microsoft Learn
- Microsoft Azure Documentation
