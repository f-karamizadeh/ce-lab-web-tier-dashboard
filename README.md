# ce-lab-web-tier-dashboard
Author: Faramarz Karamizadeh

## Overview
This repository contains the configuration and documentation for the **WebTierMonitoring** CloudWatch dashboard. Built for an Amazon Linux 2023 EC2 instance (`logging-lab`), this dashboard provides real-time visibility into system health, operational performance, and resource saturation, adhering to SRE monitoring principles.

## Dashboard Architecture & Design Decisions
The dashboard is structured into logical sections using a top-to-bottom visual hierarchy:
1. **Header & Single Value KPIs:** Quick top-level overview of active instance status and core metrics.
2. **Golden Signals & System Resources:** Monitored via EC2 infrastructure and CloudWatch Agent metrics (`CPUUtilization`, `mem_used_percent`, `disk_used_percent`, `NetworkIn`/`NetworkOut`).
3. **Correlation Views:** Overlays system utilization metrics on a shared timeline to accelerate root-cause analysis (RCA) during system degradation.

*Note on Load Balancer Metrics:* Because this setup runs directly on a single EC2 instance without an Application Load Balancer (ALB), traffic-based metrics (`RequestCount`, `TargetResponseTime`, HTTP status codes) are intentionally omitted to avoid empty noise and keep the dashboard actionable.


---
Reflection Questions & Answers
Why show P95 instead of average latency?
Averages mask extreme outliers and fail to reflect true user degradation. P95 latency accurately represents the experience of the slowest 5% of users, making it critical for SLA/SLO tracking.

What correlation patterns indicate problems?
A simultaneous spike in CPU Utilization and Memory Usage alongside reduced network throughput typically indicates thread exhaustion or resource bottlenecks under heavy load.

Why group related metrics?
Grouping related metrics (e.g., Memory, CPU, and Disk in one row) speeds up cognitive processing, allowing engineers to correlate resource pressure with system behavior instantly.

How many metrics is too many on one dashboard?
Exceeding 10–12 core widgets creates cognitive overload. Dashboards should strictly focus on actionable signals rather than raw telemetry dump.

When would you create multiple dashboards?
Separate dashboards should be created for different target audiences (e.g., high-level business/executive KPIs vs. deep-dive infrastructure troubleshooting for On-Call engineers).