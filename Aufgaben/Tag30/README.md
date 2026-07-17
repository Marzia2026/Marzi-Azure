
# Azure VPN Gateway and ExpressRoute Lab

## Overview

This lab focuses on designing and configuring hybrid network connectivity in Microsoft Azure.

The main goals are:

- Creating the network foundation for an Azure VPN Gateway
- Deploying and configuring a VPN Gateway
- Understanding Point-to-Site (P2S) VPN connections
- Understanding Site-to-Site (S2S) VPN connections
- Exploring ExpressRoute deployment options
- Comparing VPN Gateway and ExpressRoute for enterprise scenarios

---

# Lab Architecture

## Azure Network Design

Example IP Plan:

| Component | Address Range |
|---|---|
| Virtual Network | 10.10.0.0/16 |
| Workload Subnet | 10.10.1.0/24 |
| GatewaySubnet | 10.10.255.0/27 |
| P2S Client Pool | 172.16.201.0/24 |
| On-Prem Network Example | 192.168.50.0/24 |

---

# Task 1 - Prepare Azure Network Foundation

## Created Resources

Resource Group:
rg-net-lab


Virtual Network:


vnet-hq-lab


Subnets:


WorkloadSubnet
10.10.1.0/24

GatewaySubnet
10.10.255.0/27


Important:

- GatewaySubnet must have the exact name `GatewaySubnet`
- Address spaces must not overlap
- A dedicated Public IP is required for VPN Gateway

---

# Task 2 - Deploy Azure VPN Gateway

## Configuration

VPN Gateway settings:

| Setting | Value |
|-|-|
| Gateway Type | VPN |
| VPN Type | Route-based |
| SKU | Basic/Test suitable SKU |
| Connection | vnet-hq-lab |
| Public IP | Dedicated VPN Gateway IP |

## Purpose

The VPN Gateway provides:

- Point-to-Site VPN access for individual users
- Site-to-Site VPN connectivity with external networks

---

# Task 3 - ExpressRoute Evaluation

ExpressRoute was explored through the Azure portal deployment wizard.

Checked:

- Available providers
- Connectivity models
- Bandwidth options
- SKU options
- Billing models
- Peering possibilities

ExpressRoute was not deployed because it requires a real provider connection.

---

# VPN Gateway vs ExpressRoute Decision

| Criteria | VPN Gateway | ExpressRoute |
|-|-|-|
| Connection Type | Internet-based VPN tunnel | Private provider connection |
| Cost | Lower cost | Higher cost |
| Setup Time | Fast | Requires provider coordination |
| Security | Encrypted tunnel | Private connection |
| Performance | Depends on Internet | Predictable bandwidth |
| Use Case | Remote users, smaller hybrid networks | Enterprise production workloads |

---

# Task 4 - Point-to-Site VPN Configuration

## Purpose

Allow individual users to securely connect from remote locations.

Configuration:

Client Address Pool:


172.16.201.0/24


Tunnel Protocol:

Example:


OpenVPN


Authentication:

Example:


Azure AD Authentication


Possible deployment flow:

1. Configure P2S settings
2. Generate VPN client package
3. Install VPN profile on client device
4. Authenticate user
5. Connect to Azure VNet

---

# Task 5 - Site-to-Site VPN Configuration

## Components

### Local Network Gateway

Represents the on-premises network.

Example:


Name:
lng-hq-onprem

Address Space:
192.168.50.0/24

Public IP:
203.0.113.10


---

### VPN Connection

Connection:


Azure VPN Gateway
|
|
Site-to-Site VPN Tunnel
|
|
Local Network Gateway


Authentication:

Shared Key / Pre-Shared Key

Example:


StrongSharedKey123!


---

# Required On-Premises Information

For a real deployment:

- Public IP address of firewall/router
- Internal network ranges
- VPN device model
- Supported VPN protocols
- IKE version
- Encryption algorithms
- Shared key
- Routing requirements
- Firewall rules

---

# Extension Task 1 - P2S Client Deployment

VPN client package contains:

- VPN profile
- Configuration files
- Certificates (if certificate authentication is used)

Client requirements:

- Supported operating system
- VPN client software
- User authentication permission
- Network access to Azure VPN Gateway

---

# Extension Task 2 - Site-to-Site Security Checklist

## Security Risks

Weak Shared Key:

- Risk of unauthorized access
- Possible tunnel compromise
- Difficult incident investigation

## Operational Checks

Verify:

- VPN connection status in Azure Portal
- Gateway health
- Tunnel availability
- Logs and diagnostics

Recommended monitoring:

- Azure Monitor
- VPN Gateway diagnostics
- Connection health alerts

---

# Extension Task 3 - Enterprise Architecture Decision

Scenario:

Company needs:

- Headquarters connection
- Multiple branch offices
- Remote employee access

Recommended design:


Employees
|
|
Point-to-Site VPN
|
|
Azure VPN Gateway
|
|
Site-to-Site VPN
|
|
Headquarters / Branch Offices


For large enterprise:


Azure VNet
|
ExpressRoute
|
Corporate Network


Recommended combination:

- VPN Gateway:
  - Remote users
  - Small branches
  - Backup connectivity

- ExpressRoute:
  - Critical workloads
  - High bandwidth requirements
  - Predictable latency needs

---

# Key Learnings

## Point-to-Site vs Site-to-Site

Point-to-Site:

- User-to-Azure connection
- Used for remote employees
- Individual client authentication

Site-to-Site:

- Network-to-network connection
- Used for offices and data centers
- Requires VPN devices on both sides

---

# Important Azure Settings

Critical configurations:

- Correct VNet address space
- Dedicated GatewaySubnet
- Public IP configuration
- VPN Gateway SKU
- Authentication method
- Routing configuration

---

# Reflection

## 1. Difference between P2S and S2S?

P2S connects individual clients.
S2S connects complete networks.

## 2. Most critical Azure settings?

- GatewaySubnet naming
- IP planning
- VPN type
- Authentication
- Routing

## 3. When prefer ExpressRoute?

When a company requires:

- High availability
- Private connectivity
- Low latency
- Enterprise-scale hybrid networking

## 4. Required coordination before production rollout?

Need agreement with:

- Network team
- Firewall administrators
- ISP/provider
- Security team

Required information:

- IP ranges
- VPN parameters
- Authentication details
- Routing design

---

# Cleanup

After testing:

Remove unused:

- VPN Gateway
- Public IP
- Virtual Network
- Resource Group

to avoid unnecessary Azure costs.
