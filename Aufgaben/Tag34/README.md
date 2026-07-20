
# Azure Monitor, Metrics Explorer & Alerts – Practical Application Summary

## Goal
The objective of this exercise was to monitor an Azure Virtual Machine using Azure Monitor, analyze important performance metrics with Metrics Explorer, identify unusual behavior, and create meaningful alerts.

---

## Task 1: Select Target Resource

Selected Azure VM:
- VM Name: [VM-datasafe]
- Resource Group: [rg-datasafe]
- Region: [poland central]
- Operating System: [Windows]

Monitored Metrics:
- CPU Percentage
- Network In Total
- Network Out Total
- Disk Read Operations/Sec / Disk Write Operations/Sec

---

## Task 2: Metrics Explorer Visualization

Created the following charts in Azure Metrics Explorer:

1. CPU Percentage
   - Time range: Last 24 hours
   - Aggregations tested: Average / Maximum

2. Network Traffic
   - Metrics:
     - Network In Total
     - Network Out Total
   - Aggregations tested: Average / Total

3. Disk Activity
   - Metric:
     - Disk Read Operations/Sec
   - Aggregations tested: Average / Maximum

Charts were saved/pinned for future monitoring.

---

## Task 3: Metric Analysis & Anomalies

Observations:

- CPU usage was generally stable with some peak periods during higher activity.
- Network traffic increased during specific periods, showing communication activity.
- Disk operations were mostly consistent with occasional higher read/write activity.

Detected anomaly:
- A temporary CPU/network spike was observed during a short period.

Possible bottleneck:
- The VM performance was more likely limited by CPU usage rather than network or disk because CPU peaks matched periods of increased activity.

---

## Task 4: Azure Monitor Alert Configuration

Created Metric Alert:

Alert Name:
- High CPU Usage Alert

Configuration:
- Signal: CPU Percentage
- Condition: CPU > 80%
- Evaluation Period: 5 minutes
- Frequency: Every 1 minute
- Severity: Warning (Sev 2)

Reason for threshold:
- A CPU level above 80% indicates possible resource pressure while avoiding unnecessary alerts during normal operation.

Action Group:
- Email notification enabled.

---

## Task 5: Monitoring Review & Summary

Alert verification:
- Scope: Correct VM selected
- Condition: CPU threshold configured correctly
- Frequency: Appropriate for monitoring
- Action Group: Connected successfully
- Severity: Suitable for warning notification

Summary:
- The most important observed metrics were CPU, network traffic, and disk operations.
- The main unusual behavior was a temporary increase in CPU utilization.
- The CPU alert is useful because it provides an early warning before the VM becomes overloaded.
- Future monitoring recommendation:
  - Add Memory Usage monitoring and additional disk latency metrics.

---

# Extension Tasks

## Time Range Comparison

Compared:
- Last 1 hour
- Last 24 hours
- Last 7 days

Result:
- Short time ranges helped detect spikes and anomalies.
- Longer time ranges helped identify normal trends and recurring patterns.

---

## Second Alert

Created additional alert:

Metric:
- Disk Write Operations/Sec

Severity:
- Sev 3 (Informational)

Reason:
- Helps detect possible storage bottlenecks before application performance is affected.

---

## Monitoring Dashboard

Created Azure Dashboard containing:

- CPU Usage Chart
- Network Traffic Chart
- Disk Activity Chart

Dashboard Name:
- VM Performance Monitoring Dashboard

---

# Reflection

1. Which metric showed load fastest?
   - CPU Percentage was the quickest indicator of VM load.

2. Which setting changed interpretation most?
   - Time range and aggregation settings strongly affected the analysis.

3. How were anomalies identified?
   - By comparing short-term spikes with normal long-term behavior.

4. Is the alert for disruption or early warning?
   - It works mainly as an early warning system.

5. Additional future metrics:
   - Memory usage, disk latency, and application-level metrics.

6. Business-critical VM extension:
   - Add Log Analytics, Application Insights, automated scaling, and multiple alert rules.
