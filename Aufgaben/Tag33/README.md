
# Individual Learning Phase: Azure Monitor, Performance, and Basic Monitoring

## Goal

The goal of this learning phase is to gain practical experience with **Azure Monitor** and basic performance management.

The main objectives are:

- Monitor an Azure resource.
- Analyze performance metrics.
- Review logs and activity events.
- Understand the difference between metrics and logs.
- Create a basic monitoring strategy for stable operations.

---

# Requirements

- Access to Azure Portal
- Azure subscription with read permissions
- Existing Azure resource:
  - Virtual Machine
  - App Service
  - Storage Account
  - SQL Database
- Optional:
  - Log Analytics Workspace
  - Permission to create alerts and dashboards

---

# Task 1: Capture Initial Situation

## Objective

Select an Azure resource and document its current state.

## Activities

- Open Azure Portal.
- Select a resource suitable for monitoring.
- Document:

| Information | Example |
|---|---|
| Name | VM name |
| Resource Type | Virtual Machine |
| Resource Group | Resource group name |
| Region | Azure region |
| Purpose | Operational usage |

## Observation

Check:

- Availability status
- Usage information
- Current activity
- Resource overview information

## Importance of Monitoring

Monitoring helps to:

- Detect performance problems.
- Ensure availability.
- Identify configuration changes.
- Prevent unexpected failures.

---

# Task 2: Explore Azure Monitor

## Objective

Understand the main Azure Monitor functions.

## Main Monitoring Areas

| Area | Purpose |
|---|---|
| Overview | General resource information |
| Metrics | Performance measurements |
| Activity Log | Administrative events |
| Alerts | Automatic notifications |
| Logs | Detailed investigation data |

## Result

Identify which monitoring features are available for the selected resource.

---

# Task 3: Analyze Metrics

## Objective

Evaluate performance indicators and detect patterns.

## Recommended Metrics

Examples:

- CPU Usage
- Memory Usage
- Network In/Out
- Disk Read/Write
- Requests
- Availability
- Response Time

## Analysis Points

For each metric evaluate:

- Typical values
- Maximum values
- Quiet periods
- Possible causes of changes

## Result

Create a visual overview:

- Pin chart to dashboard
- Save screenshot
- Add short explanation

---

# Task 4: Review Logs and Events

## Objective

Use logs to understand changes and operational events.

## Activity Log Review

Check for:

- Starting and stopping resources
- Configuration changes
- Deployments
- Failed operations

## Log Analytics

If available:

- Open Logs section.
- Run simple queries.
- Review existing tables and events.

Example query:

```kusto
Heartbeat
| order by TimeGenerated desc
```

## Metrics vs Logs

| Metrics | Logs |
|---|---|
| Numeric measurements | Detailed records |
| Show performance trends | Explain events |
| Good for dashboards | Good for troubleshooting |

---

# Task 5: Create Monitoring Basis

## Objective

Develop simple recommendations for stable operations.

## Recommendations

### Immediately Important

- Monitor CPU and availability.
- Review important activity events.
- Configure critical alerts.

### Next Steps

- Enable diagnostic settings.
- Improve dashboards.
- Create alert rules.

### Optional Improvements

- Create workbooks.
- Extend log queries.
- Automate monitoring processes.

---

# Extension Task 1: Alert Rule

## Objective

Create automatic monitoring.

Example:

**Metric:**

CPU Percentage

**Condition:**

CPU > 80%

**Duration:**

5 minutes

**Alert Name:**

High CPU Usage Alert

If permissions are not available, document the planned alert configuration.

---

# Extension Task 2: Compare Resources

## Objective

Understand different monitoring requirements.

Example comparison:

| Category | Virtual Machine | Storage Account |
|---|---|---|
| Main Metrics | CPU, Network | Transactions, Latency |
| Risks | High CPU, downtime | Access problems |
| Logs | System events | Storage operations |
| Alerts | CPU threshold | Failed requests |

## Key Differences

- Different resources require different metrics.
- Monitoring depends on operational purpose.
- Alerts must match resource risks.

---

# Extension Task 3: Basic Log Query

## Objective

Perform simple log analysis.

Example:

```kusto
AzureActivity
| where TimeGenerated > ago(24h)
| order by TimeGenerated desc
```

Benefits:

- Shows recent activities.
- Helps troubleshooting.
- Identifies errors.
- Supports auditing.

---

# Reflection

## 1. Which metric gave the best first impression?

CPU usage because it quickly shows resource utilization.

## 2. What information comes only from logs?

Configuration changes, user actions, and detailed events.

## 3. Limits of metric-only monitoring?

Metrics show symptoms but not always the root cause.

## 4. First monitoring functions to check:

1. Metrics
2. Activity Log
3. Alerts

## 5. Best practice for stable Azure resources:

Regularly monitor important metrics, review logs, and configure alerts for critical situations.

---

# Final Result

After completing this ILP, the learner can:

- Use Azure Monitor basics.
- Analyze resource performance.
- Understand metrics and logs.
- Create simple monitoring recommendations.
- Prepare resources for stable Azure operations.
