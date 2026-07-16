
# Azure Hub & Spoke Network Topology with VNet Peering

## Overview

This lab demonstrates how to build a basic **Hub & Spoke network topology** in Microsoft Azure using **Virtual Network (VNet) Peering**.

The objective is to understand how a central Hub network can communicate with multiple Spoke networks while the Spokes remain isolated from each other because **VNet Peering is not transitive**.

---

## Learning Objectives

- Create multiple Azure Virtual Networks
- Configure Hub & Spoke architecture
- Establish VNet Peering
- Verify connectivity between Hub and Spokes
- Understand why Spoke-to-Spoke communication is not possible without additional routing

---

## Architecture

```text
                    Hub VNet
                 10.0.0.0/16
                     |
          -------------------------
          |                       |
          |                       |
   Spoke1 VNet             Spoke2 VNet
   10.1.0.0/16             10.2.0.0/16

Hub ↔ Spoke1   ✔
Hub ↔ Spoke2   ✔
Spoke1 ↔ Spoke2   ✘
```

---

# Azure Resources

| Resource | Name |
|----------|------|
| Resource Group | rg-hubspoke-lab |
| Hub VNet | vnet-hub |
| Spoke1 VNet | vnet-spoke1 |
| Spoke2 VNet | vnet-spoke2 |

---

# IP Addressing

| Network | Address Space | Subnet |
|----------|---------------|---------|
| Hub | 10.0.0.0/16 | 10.0.0.0/24 |
| Spoke1 | 10.1.0.0/16 | 10.1.0.0/24 |
| Spoke2 | 10.2.0.0/16 | 10.2.0.0/24 |

---

# Step 1 – Create a Resource Group

Create a new Resource Group.

- Name: **rg-hubspoke-lab**
- Region: West Europe (or any preferred Azure region)

---

# Step 2 – Create the Hub Virtual Network

Create the central Hub VNet.

- Name: **vnet-hub**
- Address Space: **10.0.0.0/16**
- Subnet: **10.0.0.0/24**

---

# Step 3 – Create the Spoke Virtual Networks

Create two additional VNets.

### Spoke 1

- Name: **vnet-spoke1**
- Address Space: **10.1.0.0/16**
- Subnet: **10.1.0.0/24**

### Spoke 2

- Name: **vnet-spoke2**
- Address Space: **10.2.0.0/16**
- Subnet: **10.2.0.0/24**

> **Important:** Address spaces must not overlap; otherwise VNet Peering cannot be created.

---

# Step 4 – Configure VNet Peering

Create the following peerings:

### Hub ↔ Spoke1

- hub-to-spoke1
- spoke1-to-hub

### Hub ↔ Spoke2

- hub-to-spoke2
- spoke2-to-hub

Default settings were used:

- Allow Virtual Network Access ✔
- Allow Forwarded Traffic ✘
- Gateway Transit ✘

---

# Step 5 – Verify the Configuration

Verify that all peerings show the status:

```
Connected
```

Expected result:

| VNet | Peering Status |
|------|----------------|
| Hub | Connected |
| Spoke1 | Connected |
| Spoke2 | Connected |

---

# Optional Connectivity Test

Three Ubuntu virtual machines can be deployed.

| VM | Network |
|----|----------|
| vm-hub | vnet-hub |
| vm-spoke1 | vnet-spoke1 |
| vm-spoke2 | vnet-spoke2 |

Configuration:

- Ubuntu Server LTS
- Standard B1s
- Public IP only for **vm-hub**
- Private IP only for **vm-spoke1** and **vm-spoke2**

---

# Connectivity Test

From **vm-hub**

```bash
ping <Private-IP-of-vm-spoke1>
```

Result:

```
Success
```

---

From **vm-hub**

```bash
ping <Private-IP-of-vm-spoke2>
```

Result:

```
Success
```

---

From **vm-spoke1**

```bash
ping <Private-IP-of-vm-spoke2>
```

Result:

```
Request timed out
```

---

# Why Does Spoke1 Fail to Reach Spoke2?

Azure VNet Peering is **not transitive**.

Although both Spoke networks are connected to the Hub, they are **not directly connected to each other**.

Communication between Spokes requires additional routing components such as:

- Azure Firewall
- Network Virtual Appliance (NVA)
- User Defined Routes (UDRs)

---

# Key Concepts Learned

- Hub & Spoke network topology
- Azure Virtual Networks
- VNet Peering
- Private communication over the Microsoft backbone
- Non-transitive nature of VNet Peering
- Basic Azure network design

---

# Conclusion

This lab successfully demonstrated the implementation of a basic Hub & Spoke architecture in Azure.

The Hub VNet successfully communicated with both Spoke VNets through VNet Peering. However, direct communication between Spoke networks was not possible, illustrating the non-transitive behavior of Azure VNet Peering. This design improves network organization, scalability, and security in enterprise cloud environments.
