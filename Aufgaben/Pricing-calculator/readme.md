# 🌍 Azure Pricing Calculator — Cost Analysis Project (A–F)

This project demonstrates cost estimation and optimization for Azure resources using the Azure Pricing Calculator.  
It includes virtual machines, storage, licensing models, regional pricing, and cost optimization scenarios.

---

# 📌 Project Goals

- Understand Azure pricing structure
- Compare VM costs across usage scenarios
- Evaluate Hybrid Benefit vs Pay-as-you-go
- Analyze regional price differences
- Identify cost optimization opportunities

---

# 🟦 Task A — Virtual Machine Cost & Usage

## Configuration
- Region: West Europe  
- VM: B2s (Windows)  
- Runtime: 730 hours  
- Disk: 128 GB HDD  

## 💰 Cost Breakdown

- VM (Compute + Windows): **€44.50 / month**
- Disk: **€5.50 / month**

## ⏱ Reduced Usage (160 hours/month)

- VM Cost: **€9.80**
- Savings: **€34.70**

## 📊 Summary

| Item | Cost |
|------|------|
| VM (730h) | €44.50 |
| Disk | €5.50 |
| VM (160h) | €9.80 |
| Savings | €34.70 |

---

# 🟩 Task B — Azure Hybrid Benefit

## Configuration
- VM: D2s v3 (Windows)

## 💰 Comparison

| Model | Cost |
|------|------|
| Pay-as-you-go | €165 |
| Hybrid Benefit | €95 |

## 📉 Savings
- Monthly: **€70**
- Yearly: **€840**

## 💡 When to use Hybrid Benefit
- You already own Windows Server licenses
- Long-term workloads
- Enterprise environments

---

# 🟥 Task C — Region Comparison

## VM: B2ms (Linux)

| Region | Cost |
|--------|------|
| West Europe | €72 |
| East US | €63 |
| Brazil South | €92 |

## 🏆 Results

- Cheapest: **East US**
- Most expensive: **Brazil South**

## 📈 Difference
Brazil South is **~28% more expensive** than West Europe.

---

# 🟪 Task D — VM + Storage Architecture

## Configuration
- VM: B2s (Windows)
- Storage: Blob (LRS)
- Data: 100 GB
- Disk: 128 GB SSD

## 💰 Costs

- VM: **€44.50**
- Disk: **€6.50**
- Storage: **€8.00**

## 📦 Total

➡ **€59 / month**

## 🔄 GRS Impact
- Increases cost by ~70%
- Improves geo-redundancy

---

# 🟨 Task E — Full Production Scenario

## Components

- VM1: D2s v3 (Hybrid Benefit)
- VM2: B1ms (160h)
- Storage: LRS
- SQL Database: Basic Tier

## 💰 Monthly Cost

| Component | Cost |
|----------|------|
| VM1 | €78 |
| VM2 | €18 |
| Storage | €5 |
| SQL DB | €5 |

➡ **Total: €106 / month**

## 💡 Optimization
- Reserved Instance reduces cost by ~40%

### Yearly Savings:
➡ **€372 / year**

---

# 🟥 Task F — Cost Optimization Case

## Original Setup

- VM: D8s v3 (Brazil South)
- Premium SSD (1 TB)
- GRS Storage
- 24/7 runtime

## 💰 Cost
➡ **~€900 / month**

---

## ⚠️ Cost Issues

- Overpowered VM
- Expensive region
- Premium SSD too large
- GRS unnecessary
- VM always running

---

## 🚀 Optimized Setup

- Region: West Europe
- VM: B2s
- Runtime: 180 hours/month
- Storage: LRS
- Disk: 128 GB Standard SSD

## 💰 New Cost
➡ **€45–€55 / month**

---

## 📉 Savings

➡ **~94% cost reduction**

---

# 🧠 Key Learnings

- VM runtime is the biggest cost factor
- Region selection heavily impacts pricing
- Storage redundancy increases cost significantly
- Licensing (Hybrid Benefit) reduces expenses
- Right-sizing resources is critical

---

# 📊 Conclusion

Azure cost optimization can reduce expenses by **50–95%** depending on configuration choices.

Small architectural decisions lead to major financial impact.

---
