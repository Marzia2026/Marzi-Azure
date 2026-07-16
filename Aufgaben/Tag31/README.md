
# Azure ILP – Advanced Network Security and Monitoring in Azure

## Objective
Build a secure Azure network environment using:
- Virtual Network (VNet)
- Network Security Groups (NSG)
- Azure Firewall
- Route Tables
- Azure Network Watcher

---

# Architecture

```
                    Internet
                        │
                Azure Firewall
                (afw-netsec-lab)
                        │
          -----------------------------
          │                           │
 AzureFirewallSubnet          Workload Subnet
                               (10.0.1.0/24)
                                      │
                                VM (Ubuntu)
                                      │
                                    NSG
```

---

# Resources

| Resource | Name |
|----------|------|
| Resource Group | rg-netsec-lab |
| Virtual Network | vnet-netsec-lab |
| Workload Subnet | snet-workload |
| Firewall Subnet | AzureFirewallSubnet |
| Network Security Group | nsg-workload |
| Virtual Machine | vm-workload |
| Azure Firewall | afw-netsec-lab |
| Route Table | rt-workload |

---

# Task 1 – Prepare the Lab

### Created

- Resource Group
- Virtual Network
- Two Subnets
  - snet-workload
  - AzureFirewallSubnet
- Ubuntu Linux VM

### Result

✔ Azure environment ready for security configuration.

---

# Task 2 – Configure Network Security Group

Created **nsg-workload** and associated it with the Workload subnet.

### Example Rules

| Priority | Direction | Action | Protocol | Port | Purpose |
|-----------|-----------|--------|----------|------|---------|
|100|Inbound|Allow|TCP|22|SSH administration|
|200|Inbound|Allow|TCP|80|HTTP testing|
|300|Inbound|Deny|Any|Any|Block all other inbound traffic|
|100|Outbound|Allow|Any|Any|Internet access|
|400|Outbound|Deny|TCP|23|Block Telnet|

### Result

✔ Only required traffic is permitted.

---

# Task 3 – Verify NSG

Used Azure Network Watcher.

### Tests

### Allow Test

- SSH (Port 22)
- Result: **Allowed**

### Deny Test

- Telnet (Port 23)
- Result: **Blocked**

Verified using:

- IP Flow Verify
- Effective Security Rules

### Result

✔ NSG rules worked as expected.

---

# Task 4 – Deploy Azure Firewall

Created:

- Azure Firewall
- Firewall Policy (optional)
- Route Table

Configured User Defined Route:

| Destination | Next Hop |
|--------------|----------|
|0.0.0.0/0|Azure Firewall Private IP|

Created Firewall Rule:

Example:

- Allow HTTPS (TCP 443)

or

- Allow access to microsoft.com

### Result

✔ All outbound traffic routed through Azure Firewall.

---

# Task 5 – Test Azure Firewall

Performed two tests.

### Allowed

HTTPS (443)

Result:

✔ Connection successful.

---

### Blocked

HTTP (80)

or

Blocked FQDN

Result:

✔ Connection denied.

Verified:

- Firewall Rules
- Private IP
- Route Table Association
- Monitoring information

---

# Task 6 – Azure Network Watcher

Used the following tools:

## Topology

Visualized network resources.

---

## IP Flow Verify

Confirmed which NSG rule allowed or denied traffic.

---

## Next Hop

Verified outbound traffic path.

Result:

```
VM
 ↓
Azure Firewall
 ↓
Internet
```

---

## Effective Security Rules

Displayed all active NSG rules.

---

## Connection Troubleshoot

Verified VM connectivity to external destinations.

---

# Extension Tasks

## Extension 1

Separated responsibilities:

### NSG

- Port filtering
- Network segmentation

### Azure Firewall

- Outbound traffic inspection
- Central security policy

---

## Extension 2

Added another VM or subnet.

Applied additional NSG and Firewall rules.

Validated using Network Watcher.

---

## Extension 3

Created an intentional configuration error:

Examples:

- Incorrect NSG priority
- Missing Route Table association
- Firewall rule too restrictive

Used Network Watcher to identify the issue and restored the correct configuration.

---

# Lessons Learned

- NSG protects subnets and NICs.
- Azure Firewall centrally controls network traffic.
- Route Tables determine the traffic path.
- Network Watcher is essential for troubleshooting.
- Effective Security Rules help identify which rule is applied.
- IP Flow Verify quickly explains Allow or Deny decisions.

---

# Cost Optimization

- Used **B1s** VM.
- Deployed Azure Firewall only for testing.
- Deleted all resources after completing the lab.

---

# Screenshots

- Resource Group
- Virtual Network
- Subnets
- Virtual Machine
- NSG Rules
- Azure Firewall Overview
- Route Table
- IP Flow Verify
- Next Hop
- Effective Security Rules
- Topology
- Connection Troubleshoot

---

# Reflection

- **NSG** is best for subnet/NIC-level access control.
- **Azure Firewall** provides centralized traffic management.
- **IP Flow Verify** and **Next Hop** were the most useful troubleshooting tools.
- Route Tables had the greatest impact on traffic flow.
- The architecture can easily scale by adding more subnets, NSGs, and Firewall rules for different workloads.
