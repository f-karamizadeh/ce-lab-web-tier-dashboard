Dashboard Hierarchy:
```
┌────────────────────────────────────────────┐
│ WEB TIER HEALTH - Production              │ ← Header
├────────────────────────────────────────────┤
│ 🔴 Active Alerts: 2                        │ ← Critical Info
│ System Status: ⚠️ DEGRADED                │
├────────────────────────────────────────────┤
│ [Request Rate]  │  [Error Rate]            │ ← Golden
│                 │                          │   Signals
│ [Latency P95]   │  [Target Health]         │
├────────────────────────────────────────────┤
│ [CPU]  │ [Memory]  │ [Network]  │ [Disk]  │ ← Resources
├────────────────────────────────────────────┤
│ [Request Rate + Error Rate Correlation]    │ ← Correlation
└────────────────────────────────────────────┘
```
- Key Metrics to Include:

- Request rate (requests/minute)
- Error rate (% and count)
- Latency (P50, P95, P99)
- Target health (healthy target count)
- CPU utilization
- Memory utilization
- Network throughput
- Disk usage

---
### Widget Object Keys: every entry in the widgets array, text or metric, shares the same outer shape, then branches by type:

- type: "text" or "metric"
- x, y: position in a 24 column grid, y grows downward
- width, height: size in grid units
- properties: everything else about the widget, its contents depend on type
### For text widgets, properties has one key that matters:

- markdown: the content, supports standard markdown
### For metric widgets, properties can include:

- title: chart title
- metrics: the array of series to plot, see below
- view: "timeSeries" for a line chart, "singleValue" for the KPI tiles at the top
- region: which AWS region to query
- period: seconds per datapoint
- stacked: true stacks the series instead of overlaying them, used on Errors - HTTP Status Codes
- stat: a widget level default statistic, redundant with the per-metric stat below but present on the Traffic - Request Rate widget
- yAxis: left and right axis config, label, min, max, showUnits
- annotations: horizontal and vertical reference lines, covered in Part 5
- setPeriodToTimeRange: true makes a singleValue tile average over the whole selected time range instead of just the latest period, used on P95 Latency (ms)