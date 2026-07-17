
# Azure Network Security Lab – Segmented Network Design

## Project Goal

This project demonstrates how to design a secure and segmented Azure network environment.

Main objectives:

- Transfer VLAN concepts into Azure Subnets
- Create security zones
- Control traffic using NSGs and Azure Firewall
- Prepare VPN connectivity
- Plan IDS/IPS protection

---

# Network Architecture Overview

## Virtual Network


Address Space:
10.20.0.0/16


The network is divided into different security zones:

| Zone | Purpose |
|---|---|
| Frontend | Public web application services |
| Backend | Internal application and database services |
| Management | Administrative access |
| VPN/Gateway | External secure connectivity |

---

# Subnet Design

| Subnet | Address Range | Purpose |
|---|---|---|
| snet-frontend | 10.20.1.0/24 | Public web services |
| snet-backend | 10.20.2.0/24 | Internal services |
| snet-management | 10.20.3.0/24 | Administration |
| GatewaySubnet | 10.20.250.0/27 | VPN Gateway |
| AzureFirewallSubnet | 10.20.254.0/26 | Azure Firewall |

---

# Security Zones

## 1. Frontend Zone

Purpose:

- Hosts web-facing services
- Only public accessible zone

Allowed:


Internet → HTTPS (443)


Blocked:


Internet → Backend
Internet → Management
Frontend → Management


Protection:

- NSG
- Azure Firewall
- Optional WAF

---

## 2. Backend Zone

Purpose:

- Application servers
- Database services
- Internal workloads

Allowed:


Frontend → Backend
(Only required ports)


Blocked:


Internet → Backend
Direct user access


Protection:

- NSG
- Azure Firewall

---

## 3. Management Zone

Purpose:

- Administrative resources
- Jump server
- Management tools

Allowed:


VPN Users → Management


Blocked:


Internet → Management


Protection:

- NSG
- VPN
- Azure Bastion (optional)

---

## 4. VPN Gateway Zone

Reserved subnet:


GatewaySubnet
10.20.250.0/27


Purpose:

- Site-to-Site VPN
- Point-to-Site VPN

---

# Azure Resources

## Resource Group

Example:


rg-netsec-lab


Contains:

- Virtual Network
- Subnets
- NSGs
- Firewall Policy
- VPN Resources

---

## Virtual Network

Name:


vnet-netsec


Address:


10.20.0.0/16


---

# Network Security Groups (NSG)

## Frontend NSG

Allow:


Internet → Frontend
HTTPS 443


Deny:


Frontend → Management
Frontend → Backend (except required traffic)


---

## Backend NSG

Allow:


Frontend → Backend
Required application ports


Deny:


Internet → Backend


---

## Management NSG

Allow:


VPN/Admin → Management


Deny:


Internet → Management


---

# Firewall Concept

## Firewall Types

### Packet Filtering Firewall

Purpose:

- Filters IP addresses and ports

Azure Example:


Network Security Group (NSG)


---

### Stateful Firewall

Purpose:

- Tracks active connections
- Provides advanced traffic inspection

Azure Example:


Azure Firewall


---

### Application Firewall

Purpose:

- Protects HTTP/HTTPS applications

Azure Example:


Azure Web Application Firewall (WAF)


---

# Azure Firewall Design

Firewall location:


AzureFirewallSubnet


Firewall Policy:


fwp-netsec


---

## Network Rules

Examples:

- Allow VPN management traffic
- Allow backend communication

---

## Application Rules

Examples:

- Control HTTPS access
- Restrict web traffic

---

# VPN Design

## Branch Office Connection

Requirement:

Permanent connection

Solution:


Site-to-Site IPsec VPN


Azure Components:

- Azure VPN Gateway
- Local Network Gateway

Reason:

- Fixed public IP
- Always connected

---

## Remote Administrator Access

Requirement:

Temporary secure access

Solution:


Point-to-Site VPN


Technology:


SSL VPN


Reason:

- Works from home/hotel networks
- No fixed IP required

---

# IDS / IPS Planning

## IDS

Purpose:

- Detect suspicious activities
- Generate alerts

Passive security approach.

---

## IPS

Purpose:

- Detect and block attacks

Active protection approach.

---

Recommended solution:


Azure Firewall Premium
+
IDPS Feature


Placement:


Between Internet/VPN and internal networks


---

# Traffic Security Summary

| Traffic Flow | Decision |
|---|---|
| Internet → Frontend HTTPS | Allow |
| Internet → Backend | Block |
| Internet → Management | Block |
| Frontend → Backend | Limited Allow |
| Frontend → Management | Block |
| VPN Admin → Management | Allow |
| Branch Office → Azure | Allow via IPsec |

---

# Security Principles

- Do not expose Backend directly to Internet
- Do not expose Management directly to Internet
- Use NSG for subnet-level security
- Use Firewall for central inspection
- Use VPN for secure external access
- Follow least privilege communication
- Document every security rule

---

# Reflection Notes

## VLAN vs Azure Subnet

Azure Subnets are similar to VLANs:

- Logical network separation
- Security boundaries
- Controlled communication

Difference:

- Azure uses cloud networking instead of physical switches.

---

## NSG vs Firewall

### NSG

Used for:

- Subnet protection
- Basic traffic filtering
- Internal segmentation


### Azure Firewall

Used for:

- Central traffic inspection
- Internet protection
- Advanced security rules

---

# Future Improvements

Possible improvements:

- Azure Bastion for administration
- Web Application Firewall
- Private Endpoints
- Azure Monitor
- Microsoft Sentinel
- Backup and Disaster Recovery
