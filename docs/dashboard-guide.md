# WebTierMonitoring Dashboard Guide

This guide provides operational documentation for engineers monitoring the **WebTierMonitoring** CloudWatch dashboard.

---

## 1. Dashboard Structure & Layout

The dashboard is organized top-to-bottom to enable rapid triage:

1. **Header Section:** Contains environment metadata, operational links, and quick-reference info.
2. **Resource Utilization Section:** Tracks core system metrics (CPU, Memory, Network, Disk) collected via AWS EC2 and CloudWatch Agent (`CWAgent`).
3. **Correlation View:** Combines CPU, Memory, and Network traffic into a single multi-axis chart for root-cause analysis (RCA).

---

## 2. Key Metrics & Thresholds

| Metric Name | Source | Warning Threshold | Critical Threshold | Recommended Action |
| :--- | :--- | :--- | :--- | :--- |
| **CPU Utilization** | `AWS/EC2` | `> 80%` | `> 95%` | Check active processes, scale up instance, or inspect thread locks. |
| **Memory Usage** | `CWAgent` | `> 80%` | `> 90%` | Check for application memory leaks; restart process if necessary. |
| **Disk Space Used** | `CWAgent` | `> 75%` | `> 90%` | Clear application logs or extend EBS volume size. |
| **Network In/Out** | `AWS/EC2` | N/A (Baseline deviation) | Unusually high spike | Verify if node is experiencing a traffic surge or DDoS attempt. |

---

## 3. How to Conduct Root Cause Analysis (RCA)

When responding to an incident, follow these steps using the **Correlation View**:

1. **Check for Resource Pressure:** Look at CPU and Memory trends simultaneously. A sharp CPU spike accompanied by 100% Memory indicates process swapping or execution bottlenecks.
2. **Review Disk Trends:** Ensure log files aren't rapidly consuming disk capacity, which can freeze the Python application server.
3. **Correlate with Network:** Compare CPU usage against `NetworkIn`. If CPU spikes without a corresponding increase in Network traffic, investigate internal process loops or background tasks rather than external traffic.

---

## 4. Time Range Selection & Refresh

* **Default View:** Set the dashboard time window to **Last 3 Hours** for real-time monitoring.
* **Incident Investigation:** Expand the time range to **Last 24 Hours** or **Custom Range** to identify baseline trends and previous anomaly patterns.
* **Auto-Refresh:** Enable **Auto-refresh (1m)** in the top right corner of CloudWatch to maintain live visibility during active debugging.