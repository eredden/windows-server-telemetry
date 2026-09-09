## Overview

This Grafana dashboard shows CPU utilization (%), memory utilization (%), non-paged memory pool size (bytes), disk space utilization (%), disk latency (ms), and the handle count (shortened number) of a single targeted Windows server. You are able to declare the server host name that you would like to see metrics from using the Server Name search bar at the top left.

![The Windows Server telemetry dashboard.](.\assets\dashboard.png)

## Setup

You can find the dashboard JSON file in the root of this repository as `windows-telemetry-grafana-dashboard.json`. Open the Dashboards menu in Grafana and use the *Import dashboard* button to copy the contents of the JSON file. That's the whole process!

![The Import dashboard button.](.\assets\import.png)

## Requirements

This dashboard expects a Prometheus database as the data source. The Prometheus database must have data from the following **prometheus.exporter.windows** collectors: **cpu**, **memory**, **logical_disk**, **net**, and **process**. An example of these collectors being used in a Grafana Alloy configuration file is presented below:

```alloy
// Enable the Windows performance counter collectors.
prometheus.exporter.windows "pc_metrics" {
  enabled_collectors = ["cpu", "memory", "logical_disk", "net", "process"]
}
```

I have a Raspberry Pi 4B which I flashed with the headless DietPI flavor of the Debian Linux distribution. I used the DietPI software utilities to pull down Grafana and Prometheus, configured them both minimally, and then set up Grafana Alloy on my personal machine to push telemetry to the Prometheus database. You can find the full sample config.alloy that I used for my DietPI instance in `/config/config.alloy`. 

You should be able to use this dashboard without issue regardless of whether you pull or push telemetry, so long as you are using the expected collectors.

## Attribution

This dashboard was created by [Evan Redden](https://www.linkedin.com/in/eredden). Use it however you want, but don't blame me if something goes wrong! See `LICENSE.MD` for additional information.