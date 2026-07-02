
# Individual Learning Phase (ILP)
# Understanding, Analyzing, and Controlling Azure Costs
---

# Table of Contents

1. Current State Assessment
2. Azure Pricing Models
3. Azure Cost Analysis
4. Azure Cost Factors
5. Budget and Cost Control
6. Extension Task 1
7. Extension Task 2
8. Extension Task 3
9. Reflection Questions

---

# Task 1 – Current State Assessment

## Objective

Gain an overview of the Azure subscription and available cost management features.

## Subscription Information

| Item | Result |
|------|---------|
| Subscription Name |Azure for students |
| Subscription Type | pay as you go |
| Billing Model | Azure for Students |
| Cost Period | Current Month / Last 30 Days |
| Cost Analysis | Yes / No |
| Budgets | Yes / No |
| Exports | Yes / No |
| Existing Resources | rg-mynet |
| User Permissions | Reader / Contributor / Owner |

## Observations

- Cost Management availability:yes Available
- Existing Azure resources: yes
- Permission level: Owner

---

# Task 2 – Azure Pricing Models

## Scenario

A small Azure environment consists of:

- 1 Virtual Machine
- 1 Storage Account
- Outbound Data Transfer

---

## Option 1 – Pay-As-You-Go

### Billing

| Resource | Billing Unit |
|------------|----------------|
| Virtual Machine | Per Hour |
| Storage | Per GB/Month |
| Data Transfer | Per GB |

### Advantages

- No long-term commitment
- High flexibility
- Ideal for testing

### Disadvantages

- Higher long-term costs

---

## Option 2 – Reserved Instance

### Billing

| Resource | Billing Unit |
|------------|----------------|
| Virtual Machine | 1-Year Reservation |
| Storage | Reserved Capacity |

### Advantages

- Lower monthly costs
- Better for production

### Disadvantages

- Long-term commitment required

---

## Option 3 – Different VM Sizes

| VM Size | Suitable For |
|----------|---------------|
| B2s | Development / Testing |
| D2s_v5 | Production |

---

## Comparison

| Feature | Pay-As-You-Go | Reserved |
|------------|--------------|-------------|
| Billing | Per Hour | Annual Commitment |
| Flexibility | High | Low |
| Cost | Higher | Lower |
| Test Environment | ✔ | ✖ |
| Production | ✖ | ✔ |

---

# Task 3 – Azure Cost Analysis

## Period

Last 30 Days

---

## Cost by Resource

| Resource | Cost |
|------------|---------|
| VM01 |€0.00 |
| Storage01 | €1.51|
| Virtual Network |€0.70 |

### Observation

The Cost Analysis showed that Storage were the main cost driver.  Virtual Machine had no cost impact, while networking costs were minimal. The Resource view provided the clearest overview of individual costs.

---

## Cost by Resource Type

| Resource Type | Cost |
|-------------------|---------|
| Virtual Machines | €0.00 |
| Storage Accounts | €1.45 |
| Networking | €0.54 |

---

## Cost by Resource Group

| Resource Group | Cost |
|-------------------|---------|
| RG-Test | €1.03 |
| RG-Production |€1.15 |

### Observation

Resourcegroups had more Cost
---

## Filters Used

- Location
- Service
- Tag


---

## Analysis Summary


Highest cost resource:

Resourcegroups (rg-newtest)


---

# Task 4 – Typical Azure Cost Factors

| Cost Factor | Found in Environment | Control Measure |
|----------------|----------------------|----------------|
| Compute | Yes / No | Resize or Stop VMs |
| Storage | Yes / No | Delete unused disks |
| Network | Yes / No | Reduce outbound traffic |
| Backup | General | Review Backup Policies |
| Licensing | General | Select appropriate licenses |

---

## Recommended Cost Control Measures

- Use consistent naming conventions.
- Separate Development and Production Resource Groups.
- Apply Tags for ownership and environment.
- Automatically stop test Virtual Machines.
- Review unused resources weekly.

---

# Task 5 – Budget and Warning Thresholds

## Budget Plan

| Item | Value |
|---------|----------|
| Budget Name | Monthly-Test-Budget |
| Scope | Subscription |
| Amount | €50 |
| Period | Monthly |

---

## Alert Thresholds

| Threshold | Action |
|---------------|----------------|
| 50% | Email Notification |
| 80% | Email Notification |
| 100% | Critical Alert |

---

## Notification Recipients

- Cloud Administrator
- IT Department
- Azure Owner

---

## Justification

A monthly budget helps detect unexpected spending early and improves overall cost control.

---

# Extension Task 1 – Mini Cost Report

## Reporting Period

Current Month

---

## Main Cost Sources

- Virtual Machines
- Storage Accounts
- Networking

---

## Main Cost Drivers

- Compute
- Storage Capacity
- Outbound Traffic

---

## Recommended Improvements

- Stop unused VMs
- Apply Tags
- Delete unused Storage
- Review Cost Analysis Weekly
- Create Budget Alerts

---

## Budget Status

Monthly Budget Planned

Budget Amount:

€50

Alert Levels:

- 50%
- 80%
- 100%

---

# Extension Task 2 – Savings Potential

## Example Environment

- 2 Virtual Machines
- 1 Storage Account
- 1 Virtual Network

---

## Immediate Actions

| Action | Reason |
|------------|-------------|
| Stop unused VMs | Saves Compute Costs |
| Delete unused disks | Reduces Storage Costs |
| Apply Tags | Better Cost Tracking |

---

## Medium-Term Actions

| Action | Reason |
|------------|-------------|
| Resize VMs | Lower Compute Costs |
| Weekly Cost Review | Detect Waste |

---

## Permission Required

| Action | Reason |
|------------|--------------|
| Reserved Instances | Long-term Savings |
| Azure Policy | Governance |
| Automatic Shutdown | Operational Control |

---

# Extension Task 3 – Pricing Model Comparison

## Selected Service

Azure Virtual Machine

---

### Flexible Pricing

Pay-As-You-Go

Best for:

- Development
- Testing
- Temporary workloads

---

### Long-Term Pricing

Reserved Instance

Best for:

- Production
- Continuous workloads

---

## Risk

Choosing Reserved Instances for temporary workloads may result in unnecessary expenses if resources are no longer required.

---

# Reflection Questions

## 1. Which cost view in Azure Portal was most useful?

The Resource view was the most useful because it clearly showed the cost of each individual Azure resource.

---

## 2. Which Azure services are the biggest cost drivers?

Virtual Machines are typically the highest cost driver, followed by Storage Accounts and Network traffic.

---

## 3. Where is consumption-based billing beneficial?

Consumption-based billing is highly beneficial for development and testing environments because customers only pay for the resources they actually use.

However, it can make budgeting more difficult because monthly costs may fluctuate depending on resource usage.

---

## 4. Which cost control measure would you implement first?

I would immediately implement a monthly budget with alerts at 50%, 80%, and 100%. Additionally, I would configure automatic shutdown for development Virtual Machines.

---

## 5. What would you like to learn next?

I would like to gain more experience with:

- Azure Cost Management
- Azure Reservations
- Azure Savings Plans
- Azure Advisor Cost Recommendations
- FinOps Best Practices

---

# Conclusion

Azure Cost Management provides powerful tools to monitor, analyze, and optimize cloud spending.

Using budgets, alerts, tagging strategies, and regular cost analysis helps organizations maintain predictable cloud expenses while maximizing resource efficiency.
