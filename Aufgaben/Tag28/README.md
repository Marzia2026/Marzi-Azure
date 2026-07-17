
# Azure Migration, Backup & Hybrid Scenario Lab

## Overview

This project is a practical learning exercise about migrating an On-Premises environment to Microsoft Azure.

The goal is to understand:

- Azure Migrate workflow
- Migration strategies (Rehost, Refactor, Replace)
- Difference between Azure Backup and Azure Site Recovery
- Designing a protection concept
- Hybrid management concepts like Azure Arc, Monitoring and Governance

---

# Scenario: Contoso Manufacturing GmbH

## Company Profile

Contoso is a small manufacturing company with around 80 employees.

The company currently operates several local servers and wants to move gradually to Azure.

## Current On-Premises Environment

| Server | Technology | Purpose |
|---|---|---|
| File Server | Windows Server 2022 | User files and shared folders |
| SQL Server | Windows Server + SQL Server | ERP Database |
| Web Server | Ubuntu Linux | Internal Web Application |

---

# Business Requirements

The company needs:

- Less hardware maintenance
- Reliable backup solution
- Low downtime for critical applications
- Disaster recovery capability
- Test migration before production migration
- Possibility of hybrid operation during transition

---

# Azure Target Vision

## File Server

Target:

- Azure Files
- Alternative: Azure VM

Migration Strategy:

**Replace**

Reason:

- Less administration
- Managed storage service
- Better scalability


## SQL Server

Target:

- Azure SQL VM
- Future option: Azure SQL Managed Instance

Migration Strategy:

**Rehost**

Reason:

- High compatibility
- Lower migration risk
- Easier first migration step


## Web Application

Target:

- Azure App Service
- Alternative: Linux Azure VM

Migration Strategy:

**Refactor**

Reason:

- Less server management
- Better cloud optimization

---

# Azure Migrate Process

Azure Migrate helps plan and execute migration.

Main steps:

1. Create Azure Migrate Project
2. Discovery of existing servers
3. Assessment
4. Dependency Analysis
5. Cost estimation
6. Select migration strategy
7. Execute migration


Example project:

```
Subscription:
Contoso Azure Subscription

Resource Group:
rg-migration-prod

Region:
West Europe
```

---

# Migration Order

## Phase 1: Web Application

Why?

- Lowest risk
- Good cloud candidate


## Phase 2: File Server

Why?

- Simple migration
- Low dependency


## Phase 3: SQL Server

Why?

- Most critical system
- Requires testing


---

# Backup vs Disaster Recovery

## Azure Backup

Purpose:

Protect data and restore previous versions.

Examples:

- Deleted files
- Database restore
- Previous file versions


## Azure Site Recovery (ASR)

Purpose:

Recover complete workloads after failure.

Examples:

- Server outage
- Datacenter failure
- Business continuity


## Simple Difference

| Backup | Disaster Recovery |
|-|-|
| Protects data | Protects services |
| Restore files/data | Restore whole workload |
| Regular recovery | Emergency recovery |
| Uses Recovery Points | Uses Replication and Failover |

---

# Workload Protection Design

| Workload | Azure Backup | Site Recovery | Reason |
|---|---|---|---|
| File Server | Yes | No | File restore is enough |
| SQL Server | Yes | Yes | Needs backup and fast recovery |
| Web Application | Yes | Yes | Requires service availability |

---

# Protection Concept: SQL Server

## Selected Workload

ERP Database

## Azure Solution

Components:

- Azure VM running SQL Server
- Recovery Services Vault
- Azure Backup
- Azure Site Recovery


## Backup Plan

- Daily backups
- Weekly full backup
- Long-term retention


## Disaster Recovery Plan

Failure scenario:

SQL Server hardware failure


Steps:

1. Detect failure
2. Start Site Recovery failover
3. Start Azure VM
4. Redirect application traffic
5. Test ERP functionality


Dependencies:

- Network connectivity
- Active Directory
- Storage performance
- Application configuration

---

# Hybrid Azure Topics

## Fundamentals (Needed First)

### Monitoring

Purpose:

- Check system health
- Detect problems


### Security

Purpose:

- Protect identities
- Protect resources


### Server Inventory

Purpose:

- Understand existing environment


### Governance

Purpose:

- Organize Azure resources


---

# Advanced Topics (Later)

## Azure Arc

Use case:

Manage servers outside Azure from Azure control plane.


Benefits:

- Central inventory
- Policy management
- Monitoring
- Security


## Centralized Policies

Used for:

- Compliance
- Standard configurations


## Configuration Management

Used for:

- Automation
- Consistent server settings


---

# Final Migration Decisions

| Workload | Decision |
|-|-|
| File Server | Replace with Azure Files |
| SQL Server | Rehost to Azure VM |
| Web Application | Refactor to Azure App Service |

---

# Mini Disaster Recovery Plan

## Trigger

- Server failure
- Data corruption
- Site outage


## Responsible Roles

- Azure Administrator
- IT Administrator
- Application Owner


## Recovery Steps

1. Identify incident
2. Start recovery process
3. Failover workload
4. Restore missing data if required
5. Validate application


---

# Azure Arc Evaluation

Possible systems:

- Remaining On-Prem servers
- Linux machines
- SQL Servers outside Azure


Benefits:

- Hybrid management
- Central monitoring
- Policy enforcement


Why later?

Because migration comes first.

Azure Arc improves management after the hybrid environment exists.

---

# Learning Results

After completing this project:

I understand:

✅ How Azure Migrate supports migration planning  
✅ How to choose between Rehost, Refactor and Replace  
✅ Difference between Backup and Disaster Recovery  
✅ When to use Azure Backup and Site Recovery  
✅ How hybrid Azure services support long-term management  


---

# Next Learning Steps

1. Practice Azure Networking:
   - Virtual Networks
   - VPN Gateway
   - Private Endpoints


2. Practice Backup and Disaster Recovery:
   - Recovery Services Vault
   - Backup Policies
   - Site Recovery


3. Learn Azure Security:
   - Microsoft Defender for Cloud
   - Microsoft Entra ID
   - Azure Policy


---

## Conclusion

This project demonstrates a realistic path from an On-Premises environment to Azure.

The migration should not only move servers to the cloud but also improve:

- Reliability
- Security
- Recovery capability
- Operational management
