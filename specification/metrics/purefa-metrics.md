# Semantic Conventions for Pure FlashArray Metrics <!-- omit from toc -->

This document describes the semantic conventions for Pure FlashArray Metrics.


<!-- toc -->

- [Collections by Endpoint](#collections-by-endpoint)
- [Metric Instruments](#metric-instruments)
  - [`purefa_info` - FlashArray System Information](#purefa_info---flasharray-system-information)
  - [`purefa_alerts` - FlashArray Alerts Information](#purefa_alerts---flasharray-alerts-information)
  - [`purefa_array` - FlashArray metrics](#purefa_array---flasharray-metrics)
  - [`purefa_directory` - FlashArray File Directory metrics](#purefa_directory---flasharray-file-directory-metrics)
  - [`purefa_host` - Host metrics](#purefa_host---host-metrics)
  - [`purefa_hw` - Hardware metrics](#purefa_hw---hardware-metrics)
  - [`purefa_pod` - Pod metrics](#purefa_pod---pod-metrics)
  - [`purefa_volume` - Volume metrics](#purefa_volume---volume-metrics)

<!-- tocstop -->

## Collections by Endpoint

| Endpoint             | Description              | Metrics Instruments collected                               |
| -------------------- | ------------------------ | ----------------------------------------------------------- |
| /metrics             | Full array metrics       | all                                                         |
| /metrics/array       | Array only metrics       | `purefa_info`, `purefa_alerts`, `purefa_array`, `purefa_hw` |
| /metrics/directories | Directories only metrics | `purefa_info`, `purefa_directory`                           |
| /metrics/hosts       | Hosts only metrics       | `purefa_info`, `purefa_host`                                |
| /metrics/pods        | Pods only metrics        | `purefa_info`, `purefa_pod`                                 |
| /metrics/volumes     | Volumes only metrics     | `purefa_info`, `purefa_volume`                              |


## Metric Instruments

### `purefa_info` - FlashArray System Information

**Description:** FlashArray System Information

| Name        | Description                   | Units | Metric Type ([*](https://github.com/OpenObservability/OpenMetrics/blob/main/specification/OpenMetrics.md#metric-types)) | Value Type | Attribute Key | Attribute Values       |
| ----------- | ----------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------- | ---------- | ------------- | ---------------------- |
| purefa_info | FlashArray system information |       | Gauge                                                                                                                   | Double     | `array_name`    | (name)                 |
|             |                               |       |                                                                                                                         |            | `os`          | (array os name)        |
|             |                               |       |                                                                                                                         |            | `system_id`   | (array system id)      |
|             |                               |       |                                                                                                                         |            | `version`     | (array purity version) |


### `purefa_alerts` - FlashArray Alerts Information

**Description:** FlashArray Open Alerts

| Name               | Description                  | Units | Metric Type ([*](https://github.com/OpenObservability/OpenMetrics/blob/main/specification/OpenMetrics.md#metric-types)) | Value Type | Attribute Key    | Attribute Values                                                                                                   |
| ------------------ | ---------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------- | ---------- | ---------------- | ------------------------------------------------------------------------------------------------------------------ |
| purefa_alerts_open | FlashArray open alert events |       | Gauge                                                                                                                   | Double     | `component_name` | (name)                                                                                                             |
|                    |                              |       |                                                                                                                         |            | `component_type` | `chassis`, `drive_bay`, `nvram_bay`, `power_supply`, `temp_sensor`, `controller`, `eth_port`, `cooling`, `fc_port` |
|                    |                              |       |                                                                                                                         |            | `severity`       | `info`, `warning`, `critical`, `hidden`                                                                            |


### `purefa_array` - FlashArray metrics

**Description:** FlashArray performance metrics

| Name                                     | Description                                   | Units             | Metric Type ([*](https://github.com/OpenObservability/OpenMetrics/blob/main/specification/OpenMetrics.md#metric-types)) | Value Type | Attribute Key | Attribute Values                                                                                                                                                                                                                                                                                                                                                                                                                             |
| ---------------------------------------- | --------------------------------------------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------- | ---------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| purefa_array_performance_latency_usec    | FlashArray array latency                      | microsecond       | Gauge                                                                                                                   | Double     | `dimension`   | `queue_usec_per_mirrored_write_op`, `queue_usec_per_read_op`, `queue_usec_per_write_op`, `san_usec_per_mirrored_write_op`, `san_usec_per_read_op`, `san_usec_per_write_op`, `service_usec_per_mirrored_write_op`, `service_usec_per_read_op`, `service_usec_per_write_op`, `usec_per_mirrored_write_op`, `usec_per_read_op`, `usec_per_write_op`, `service_usec_per_read_op_cache_reduction`, `local_queue_usec_per_op`, `usec_per_other_op` |
| purefa_array_performance_throughput_iops | FlashArray array throughput                   | operations/second | Gauge                                                                                                                   | Double     | `dimension`   | `mirrored_writes_per_sec`, `reads_per_sec`, `writes_per_sec`, `others_per_sec`                                                                                                                                                                                                                                                                                                                                                               |
| purefa_array_performance_bandwidth_bytes | FlashArray array throughput                   | bytes/second      | Gauge                                                                                                                   | Double     | `dimension`   | `mirrored_write_bytes_per_sec`, `read_bytes_per_sec`, `write_bytes_per_sec`                                                                                                                                                                                                                                                                                                                                                                  |
| purefa_array_performance_average_bytes   | FlashArray array average operations size      | bytes/operation   | Gauge                                                                                                                   | Double     | `dimension`   | `bytes_per_mirrored_write`, `bytes_per_op`, `bytes_per_read`, `bytes_per_write`                                                                                                                                                                                                                                                                                                                                                              |
| purefa_array_performance_queue_depth_ops | FlashArray array queue depth size             | operations        | Gauge                                                                                                                   | Double     |               |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| purefa_array_space_data_reduction_ratio  | FlashArray array space data reduction         | ratio             | Gauge                                                                                                                   | Double     |               |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| purefa_array_space_bytes                 | FlashArray array space in bytes               | bytes             | Gauge                                                                                                                   | Double     | `space`       | `capacity`, `shared`, `snapshots`, `system`, `thin_provisioning`, `total_physical`, `total_provisioned`, `total_reduction`, `unique`, `virtual`, `replication`, `shared_effective`, `snapshots_effective`, `unique_effective`, `total_effective`, `empty`                                                                                                                                                                                    |
| purefa_array_space_utilization           | FlashArray array space utilization in percent | ratio             | Gauge                                                                                                                   | Double     |


### `purefa_directory` - FlashArray File Directory metrics

**Description:** TODO


### `purefa_host` - Host metrics

**Description:** FlashArray connected host metrics

| Name                                    | Description                                         | Units             | Metric Type ([*](https://github.com/OpenObservability/OpenMetrics/blob/main/specification/OpenMetrics.md#metric-types)) | Value Type | Attribute Key | Attribute Values                                                                                                                                                                                                                                                                                                                                                                             |
| --------------------------------------- | --------------------------------------------------- | ----------------- | ----------------------------------------------------------------------------------------------------------------------- | ---------- | ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| purefa_host_connections_info            | FlashArray host volumes connections                 |                   | Gauge                                                                                                                   | Double     | `host`        | (host name)                                                                                                                                                                                                                                                                                                                                                                                  |
|                                         |                                                     |                   |                                                                                                                         |            | `hostgroup`   | (hostgroup name)                                                                                                                                                                                                                                                                                                                                                                             |
|                                         |                                                     |                   |                                                                                                                         |            | `volume`      | (volume name)                                                                                                                                                                                                                                                                                                                                                                                |
| purefa_host_performance_latency_usec    | FlashArray host latency                             | microsecond       | Gauge                                                                                                                   | Double     | `host`        | (host name)                                                                                                                                                                                                                                                                                                                                                                                  |
|                                         |                                                     |                   |                                                                                                                         |            | `dimension`   | `queue_usec_per_mirrored_write_op`, `queue_usec_per_read_op`, `queue_usec_per_write_op`, `san_usec_per_mirrored_write_op`, `san_usec_per_read_op`, `san_usec_per_write_op`, `service_usec_per_mirrored_write_op`, `service_usec_per_read_op`, `service_usec_per_write_op`, `usec_per_mirrored_write_op`, `usec_per_read_op`, `usec_per_write_op`, `service_usec_per_read_op_cache_reduction` |
| purefa_host_performance_throughput_iops | FlashArray host throughput in operations per second | operations/second | Gauge                                                                                                                   | Double     | `host`        | (host name)                                                                                                                                                                                                                                                                                                                                                                                  |
|                                         |                                                     |                   |                                                                                                                         |            | `dimension`   | `mirrored_writes_per_sec`, `reads_per_sec`, `writes_per_sec`                                                                                                                                                                                                                                                                                                                                 |
| purefa_host_performance_bandwidth_bytes | FlashArray host throughput in bytes                 | bytes/second      | Gauge                                                                                                                   | Double     | `host`        | (host name)                                                                                                                                                                                                                                                                                                                                                                                  |
|                                         |                                                     |                   |                                                                                                                         |            | `dimension`   | `mirrored_write_bytes_per_sec`, `read_bytes_per_sec`, `write_bytes_per_sec`                                                                                                                                                                                                                                                                                                                  |
| purefa_host_performance_average_bytes   | FlashArray host average operations size in bytes    | bytes/operation   | Gauge                                                                                                                   | Double     | `host`        | (host name)                                                                                                                                                                                                                                                                                                                                                                                  |
|                                         |                                                     |                   |                                                                                                                         |            | `dimension`   | `bytes_per_mirrored_write`, `bytes_per_op`, `bytes_per_read`, `bytes_per_write`                                                                                                                                                                                                                                                                                                              |
| purefa_host_space_bytes                 | FlashArray host space in bytess                     | bytes             | Gauge                                                                                                                   | Double     | `host`        | (host name)                                                                                                                                                                                                                                                                                                                                                                                  |
|                                         |                                                     |                   |                                                                                                                         |            | `space`       | `shared`, `snapshots`, `system`, `thin_provisioning`, `total_physical`, `total_provisioned`, `total_reduction`, `unique`, `virtual`, `replication`, `shared_effective`, `snapshots_effective`, `unique_effective`, `total_effective`                                                                                                                                                         |
| purefa_host_space_data_reduction_ratio  | FlashArray host space data reduction                | ratio             | Gauge                                                                                                                   | Double     | `host`        | (host name)                                                                                                                                                                                                                                                                                                                                                                                  |


### `purefa_hw` - Hardware metrics

**Description:** FlashArray hardware metrics
| Name                                    | Description                               | Units | Metric Type ([*](https://github.com/OpenObservability/OpenMetrics/blob/main/specification/OpenMetrics.md#metric-types)) | Value Type | Attribute Key      | Attribute Values                                                                                                   |
| --------------------------------------- | ----------------------------------------- | ----- | ----------------------------------------------------------------------------------------------------------------------- | ---------- | ------------------ | ------------------------------------------------------------------------------------------------------------------ |
| purefa_hw_component_status              | FlashArray hardware component status      |       | Gauge                                                                                                                   | int        | `component_name`   | (component name)                                                                                                   |
|                                         |                                           |       |                                                                                                                         |            | `component_type`   | `chassis`, `drive_bay`, `nvram_bay`, `power_supply`, `temp_sensor`, `controller`, `eth_port`, `cooling`, `fc_port` |
|                                         |                                           |       |                                                                                                                         |            | `component_status` | `ok`, `critical`, `degraded`, `device_off`, `identifying`, `not_installed`, `unknown`                              |
| purefa_hw_component_temperature_celsius | FlashArray hardware component temperature | Cel   | Gauge                                                                                                                   | Double     | `component_name`   | (name)                                                                                                             |
|                                         |                                           |       |                                                                                                                         |            | `component_type`   | `temp_sensor`                                                                                                      |
| purefa_hw_component_voltage_volt        | FlashArray hardware component voltage     |       | Gauge                                                                                                                   | Double     | `component_name`   | (name)                                                                                                             |
|                                         |                                           |       |                                                                                                                         |            | `component_type`   | `power_supply`                                                                                                     |



### `purefa_pod` - Pod metrics

**Description:** TODO


### `purefa_volume` - Volume metrics

**Description:** TODO