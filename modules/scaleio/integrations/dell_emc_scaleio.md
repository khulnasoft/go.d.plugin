<!--startmeta
custom_edit_url: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/scaleio/README.md"
meta_yaml: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/scaleio/metadata.yaml"
sidebar_label: "Dell EMC ScaleIO"
learn_status: "Published"
learn_rel_path: "Collecting Metrics/Storage, Mount Points and Filesystems"
most_popular: False
message: "DO NOT EDIT THIS FILE DIRECTLY, IT IS GENERATED BY THE COLLECTOR'S metadata.yaml FILE"
endmeta-->

# Dell EMC ScaleIO


<img src="https://khulnasoft.com/img/dell.svg" width="150"/>


Plugin: go.d.plugin
Module: scaleio

<img src="https://img.shields.io/badge/maintained%20by-Khulnasoft-%2300ab44" />

## Overview

This collector monitors ScaleIO (VxFlex OS) instances via VxFlex OS Gateway API.

It collects metrics for the following ScaleIO components:

- System
- Storage Pool
- Sdc




This collector is supported on all platforms.

This collector supports collecting metrics from multiple instances of this integration, including remote instances.


### Default Behavior

#### Auto-Detection

This integration doesn't support auto-detection.

#### Limits

The default configuration for this integration does not impose any limits on data collection.

#### Performance Impact

The default configuration for this integration is not expected to impose a significant performance impact on the system.


## Metrics

Metrics grouped by *scope*.

The scope defines the instance that the metric belongs to. An instance is uniquely identified by a set of labels.



### Per Dell EMC ScaleIO instance

These metrics refer to the entire monitored application.

This scope has no labels.

Metrics:

| Metric | Dimensions | Unit |
|:------|:----------|:----|
| scaleio.system_capacity_total | total | KiB |
| scaleio.system_capacity_in_use | in_use | KiB |
| scaleio.system_capacity_usage | thick, decreased, thin, snapshot, spare, unused | KiB |
| scaleio.system_capacity_available_volume_allocation | available | KiB |
| scaleio.system_capacity_health_state | protected, degraded, in_maintenance, failed, unavailable | KiB |
| scaleio.system_workload_primary_bandwidth_total | total | KiB/s |
| scaleio.system_workload_primary_bandwidth | read, write | KiB/s |
| scaleio.system_workload_primary_iops_total | total | iops/s |
| scaleio.system_workload_primary_iops | read, write | iops/s |
| scaleio.system_workload_primary_io_size_total | io_size | KiB |
| scaleio.system_rebalance | read, write | KiB/s |
| scaleio.system_rebalance_left | left | KiB |
| scaleio.system_rebalance_time_until_finish | time | seconds |
| scaleio.system_rebuild | read, write | KiB/s |
| scaleio.system_rebuild_left | left | KiB |
| scaleio.system_defined_components | devices, fault_sets, protection_domains, rfcache_devices, sdc, sds, snapshots, storage_pools, volumes, vtrees | components |
| scaleio.system_components_volumes_by_type | thick, thin | volumes |
| scaleio.system_components_volumes_by_mapping | mapped, unmapped | volumes |

### Per storage pool

These metrics refer to the storage pool.

This scope has no labels.

Metrics:

| Metric | Dimensions | Unit |
|:------|:----------|:----|
| scaleio.storage_pool_capacity_total | total | KiB |
| scaleio.storage_pool_capacity_in_use | in_use | KiB |
| scaleio.storage_pool_capacity_usage | thick, decreased, thin, snapshot, spare, unused | KiB |
| scaleio.storage_pool_capacity_utilization | used | percentage |
| scaleio.storage_pool_capacity_available_volume_allocation | available | KiB |
| scaleio.storage_pool_capacity_health_state | protected, degraded, in_maintenance, failed, unavailable | KiB |
| scaleio.storage_pool_components | devices, snapshots, volumes, vtrees | components |

### Per sdc

These metrics refer to the SDC (ScaleIO Data Client).

This scope has no labels.

Metrics:

| Metric | Dimensions | Unit |
|:------|:----------|:----|
| scaleio.sdc_mdm_connection_state | connected | boolean |
| scaleio.sdc_bandwidth | read, write | KiB/s |
| scaleio.sdc_iops | read, write | iops/s |
| scaleio.sdc_io_size | read, write | KiB |
| scaleio.sdc_num_of_mapped_volumed | mapped | volumes |



## Alerts

There are no alerts configured by default for this integration.


## Setup

### Prerequisites

No action required.

### Configuration

#### File

The configuration file name for this integration is `go.d/scaleio.conf`.


You can edit the configuration file using the `edit-config` script from the
Khulnasoft [config directory](https://github.com/khulnasoft/khulnasoft/blob/master/docs/khulnasoft-agent/configuration.md#the-khulnasoft-config-directory).

```bash
cd /etc/khulnasoft 2>/dev/null || cd /opt/khulnasoft/etc/khulnasoft
sudo ./edit-config go.d/scaleio.conf
```
#### Options

The following options can be defined globally: update_every, autodetection_retry.


<details><summary>Config options</summary>

| Name | Description | Default | Required |
|:----|:-----------|:-------|:--------:|
| update_every | Data collection frequency. | 5 | no |
| autodetection_retry | Recheck interval in seconds. Zero means no recheck will be scheduled. | 0 | no |
| url | Server URL. | https://127.0.0.1:80 | yes |
| timeout | HTTP request timeout. | 1 | no |
| username | Username for basic HTTP authentication. |  | yes |
| password | Password for basic HTTP authentication. |  | yes |
| proxy_url | Proxy URL. |  | no |
| proxy_username | Username for proxy basic HTTP authentication. |  | no |
| proxy_password | Password for proxy basic HTTP authentication. |  | no |
| method | HTTP request method. | GET | no |
| body | HTTP request body. |  | no |
| headers | HTTP request headers. |  | no |
| not_follow_redirects | Redirect handling policy. Controls whether the client follows redirects. | no | no |
| tls_skip_verify | Server certificate chain and hostname validation policy. Controls whether the client performs this check. | no | no |
| tls_ca | Certification authority that the client uses when verifying the server's certificates. |  | no |
| tls_cert | Client TLS certificate. |  | no |
| tls_key | Client TLS key. |  | no |

</details>

#### Examples

##### Basic

An example configuration.

<details><summary>Config</summary>

```yaml
jobs:
  - name: local
    url: https://127.0.0.1
    username: admin
    password: password
    tls_skip_verify: yes  # self-signed certificate

```
</details>

##### Multi-instance

> **Note**: When you define multiple jobs, their names must be unique.

Local and remote instance.


<details><summary>Config</summary>

```yaml
jobs:
  - name: local
    url: https://127.0.0.1
    username: admin
    password: password
    tls_skip_verify: yes  # self-signed certificate

  - name: remote
    url: https://203.0.113.10
    username: admin
    password: password
    tls_skip_verify: yes

```
</details>



## Troubleshooting

### Debug Mode

To troubleshoot issues with the `scaleio` collector, run the `go.d.plugin` with the debug option enabled. The output
should give you clues as to why the collector isn't working.

- Navigate to the `plugins.d` directory, usually at `/usr/libexec/khulnasoft/plugins.d/`. If that's not the case on
  your system, open `khulnasoft.conf` and look for the `plugins` setting under `[directories]`.

  ```bash
  cd /usr/libexec/khulnasoft/plugins.d/
  ```

- Switch to the `khulnasoft` user.

  ```bash
  sudo -u khulnasoft -s
  ```

- Run the `go.d.plugin` to debug the collector:

  ```bash
  ./go.d.plugin -d -m scaleio
  ```


