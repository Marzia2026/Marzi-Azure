# Individual Learning Phase

Application Monitoring and Resource Optimization with Azure
## Task 1: Prepare a Monitorable Azure Application
Environment Information
Item	Value
Resource Group	rg-monitoring-demo
Application Name	my-monitoring-webapp
Application Insights	my-monitoring-insights

Actions performed:
Created Azure Web App in a Resource Group.
Enabled Application Insights integration.
Opened the application several times to generate telemetry data.
Verified that requests were appearing in Application Insights.
Result:

The application is accessible and connected to Azure monitoring services.

## Task 2: Explore Application Insights
Checked sections:
Overview

Observation:

Application Insights displayed the total number of requests.
Average response time was visible.
No critical failures were detected initially.
Live Metrics

Observation:

Incoming requests appeared in real time.
Server response time was monitored.
Application activity increased when refreshing the webpage.
Failures

Observation:

A test request to a non-existing page generated an HTTP 404 error.
Failed requests were visible in the Failures dashboard.
Performance

Observation:

Average response duration was low.
No significant performance bottleneck was detected.
Transaction Search

Observation:

Individual requests and timestamps were visible.
Request details could be inspected.
Three Main Observations:
The application received multiple successful requests after opening the website.
Response times remained stable during normal usage.
Invalid URLs created detectable HTTP 404 failures.
## Task 3: Availability Monitoring
Availability Test Configuration
Setting	Value
Test Name	WebApp-Availability-Test
Test Type	URL ping test
Interval	5 minutes
First Status	Available / Passed
Result:

An availability test was successfully created and monitoring started.

## Task 4: Analyze Resource Usage
Metrics examined:
Application Insights:
Requests
Response Time
Failed Requests
Dependencies
App Service Metrics:
CPU Percentage
Memory Working Set
HTTP 4xx Errors
HTTP 5xx Errors
Analysis:
Metric	Observation
Requests	Low traffic during testing
CPU Usage	Below critical level
Memory Usage	Stable
Response Time	Normal response speed
HTTP Errors	Only test-generated 404 errors
Correlation:

The Application Insights data and App Service metrics matched:

Low request count resulted in low CPU usage.
No performance issues were detected.
Errors visible in Application Insights were also reflected in HTTP error metrics.
## Task 5: Azure Advisor Optimization Review
Recommendation 1
Resource:

App Service Plan

Recommendation:

Review pricing tier and scaling options.

Expected Benefit:
Lower monthly cost.
Better resource allocation.
Decision:

Review later

Reason:
Current resource usage is low, but scaling may become necessary with higher traffic.

Recommendation 2
Resource:

Application Monitoring

Recommendation:

Enable additional diagnostic logging.

Expected Benefit:
Better troubleshooting.
Faster identification of application problems.
Decision:

Implement now

Reason:
Low-risk improvement that increases visibility.

## Extension Task 1: Log Analysis
Query 1: Most frequent requests

Example KQL:

requests
| summarize RequestCount=count() by name
| order by RequestCount desc

Result:
Shows which pages or endpoints are requested most frequently.

Query 2: Failed requests
requests
| where success == false
| summarize FailedRequests=count() by resultCode

Result:
Shows HTTP errors and failure frequency.

Most useful query:

The failed requests query was the most helpful because it immediately identified application problems.

## Extension Task 2: Alerting
Alert Rule
Setting	Value
Condition	Response time too high
Threshold	Average response time > 2 seconds
Evaluation	Every 5 minutes
Action	Send email notification
Desired reaction:

Investigate performance problems and check resource usage.

Extension Task 3: Optimization Proposal
App Service Scaling Improvement
Current State:
Small App Service Plan.
Low traffic.
Manual scaling.
Planned Target State:
Enable autoscaling rules.
Increase resources automatically during high traffic.
Expected Effect:
Better performance during peak load.
Avoid unnecessary costs during low usage.
Risk:
Higher costs if scaling limits are configured incorrectly.
Reflection Questions
1. Which Application Insights view gave the quickest overview?

The Overview dashboard provided the fastest understanding because it combined requests, response time, failures, and availability information.

2. Which metrics were most helpful?

The most useful metrics were:

CPU Percentage
Response Time
Failed Requests
Request Count

They helped identify performance and availability issues.

3. Which recommendation would you implement first?

I would first implement improved monitoring and alerting because it has low risk and improves operational visibility.

4. Which monitoring data should be continuously observed?

In production I would continuously monitor:

Response time
Error rate
CPU and memory usage
Availability
Dependency failures
5. Limitations of portal-based analysis?

Limitations:

Historical analysis can be limited without proper retention settings.
Complex application problems may require deeper log analysis.
Portal dashboards may not show the full business context.
Correlation between multiple services can become difficult.
