{
  "type": "metric",
  "x": 0,
  "y": 18,
  "width": 6,
  "height": 5,
  "properties": {
    "title": "CPU Utilization",
    "metrics": [
      ["AWS/EC2", "CPUUtilization", "InstanceId", "i-05aa2b7dd63d8cbe1", {"stat": "Average"}]
    ],
    "view": "timeSeries",
    "region": "us-east-1",
    "period": 300,
    "yAxis": {
      "left": {"min": 0, "max": 100, "label": "%"}
    },
    "annotations": {
      "horizontal": [
        {"value": 80, "label": "Warning", "fill": "above", "color": "#ff7f0e"}
      ],
      "vertical": [
        {"label": "Deployment", "value": "2026-01-20T14:00:00Z", "color": "#00ff00"}
      ]
    }
  }
}