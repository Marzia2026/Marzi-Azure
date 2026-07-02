
# Azure Subscription, Management, SLA & Cost Overview

## Task 1 – Explore Azure Subscription

### Purpose
Understand the basic information of an Azure Subscription and why it is important.

| Information | Description | Why it is important |
|-------------|-------------|---------------------|
| **Display Name** | Name of the subscription | Identifies the correct subscription. |
| **Subscription ID** | Unique subscription identifier | Used in support, automation, and scripts. |
| **Status** | Current state (e.g., Active) | Indicates whether resources can be used. |
| **Directory / Tenant** | Connected Microsoft Entra ID tenant | Shows where identities and users are managed. |
| **Offer / Billing Model** | Pricing model (e.g., Pay-As-You-Go, Student) | Determines billing and subscription limits. |
| **Management Areas** | Available administration features | Provides access to security, policies, monitoring, and cost management. |

---

# Task 2 – Subscription Management Areas

| Area | Purpose | Example Administrative Task | Access |
|------|---------|-----------------------------|--------|
| **Access Control (IAM)** | Manage user permissions | Assign Owner or Contributor roles | Read & Modify |
| **Tags** | Organize resources | Add Environment or Department tags | Read & Modify |
| **Policies** | Enforce organizational rules | Require mandatory tags | Read & Modify |
| **Resource Providers** | Register Azure services | Enable Microsoft.Compute | Read & Modify |
| **Cost Management + Billing** | Monitor and control costs | Create budgets and alerts | Read & Modify |
| **Activity Log** | View subscription activities | Review resource changes | Mostly Read |

### Typical Subscription-Level Tasks

- Manage user access with IAM.
- Configure Azure Policies and Tags.
- Monitor costs and resource activities.

---

# Task 3 – Compare Azure SLAs

| Service | Typical SLA | SLA Requirement | Higher Availability |
|---------|-------------|-----------------|---------------------|
| **Azure Virtual Machines** | 99.9% | Two or more VMs in an Availability Set or Availability Zones | Use Availability Zones |
| **Azure App Service** | 99.95% | Two or more instances | Scale out to multiple instances |
| **Azure Storage** | 99.9%+ | Depends on selected redundancy option | Use GRS or RA-GRS |
| **Azure SQL Database** | 99.99% | Built-in service redundancy | Use geo-replication if required |

> **Important:** SLA percentages apply only when Microsoft's documented conditions are met.

---

# Task 4 – Cost vs Availability

## Scenario

- Small internal web application
- Used only on weekdays
- Short outages are acceptable
- Limited budget

### Variant A – Cost-Effective Solution

**Services**

- Azure App Service (Basic)
- Azure SQL Database (Basic)

**Estimated Cost**

- ~30–50 €/month

**Availability**

- Around **99.95%** (depending on configuration)

**Advantages**

- Low monthly cost
- Easy deployment
- Simple management

**Disadvantages**

- Limited redundancy
- Less protection against failures

---

### Variant B – Higher Availability Solution

**Services**

- Azure App Service (Premium)
- Azure SQL Database (Standard)
- Availability Zones

**Estimated Cost**

- ~120–200 €/month

**Availability**

- Higher availability with redundancy and multiple instances

**Advantages**

- Better fault tolerance
- Reduced downtime
- Suitable for important applications

**Disadvantages**

- Higher monthly cost
- More complex configuration

---

### Comparison

| Feature | Variant A | Variant B |
|---------|-----------|-----------|
| Cost | Low | Higher |
| Availability | Good | Very High |
| Complexity | Low | Medium |
| Best For | Internal apps | Business-critical apps |

**Summary**

Variant A is cheaper because it uses fewer resources and minimal redundancy.  
Variant B costs more because it uses multiple instances and high-availability features.  
Higher availability generally results in higher operational costs.

---

# Task 5 – Recommendation

### Recommended Approach

- Verify the **Subscription ID** and **Status** before deployment.
- Regularly monitor **IAM**, **Policies**, **Cost Management**, and **Activity Log**.
- For a small internal application, **Variant A** is recommended.
- It provides sufficient availability while keeping monthly costs low.
- Upgrade to Variant B only if downtime becomes business-critical.

---

# Extension Task 1 – Cost Control

### Useful Features

- Cost Analysis
- Budgets
- Alerts
- Exports

### Recommendation

- Create a monthly budget.
- Configure cost alerts at **80%** of the budget.
- Review Cost Analysis regularly.

---

# Extension Task 2 – SLA Pitfalls

Example: **Azure App Service**

- SLA applies only under Microsoft's documented conditions.
- Multiple instances may be required.
- Planned maintenance is not always considered downtime.
- Network issues outside Azure are excluded.
- Customer configuration errors are not covered.
- Always read SLA limitations before relying on the percentage.

---

# Extension Task 3 – Customer-Facing Application

If the application is customer-facing:

- Use Premium App Service.
- Deploy multiple instances.
- Enable Availability Zones.
- Consider Geo-redundancy and backups.

Although costs increase, availability and reliability improve significantly.

---

# Key Takeaways

- A Subscription is the administrative boundary for Azure resources.
- IAM, Policies, Tags, Cost Management, and Activity Log are essential management tools.
- SLA percentages depend on specific Microsoft conditions.
- Higher availability generally requires additional resources and higher costs.
- Choose services based on business requirements rather than SLA percentage alone.
