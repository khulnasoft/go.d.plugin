<!--startmeta
custom_edit_url: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/dnsmasq/README.md"
meta_yaml: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/dnsmasq/metadata.yaml"
sidebar_label: "Dnsmasq"
learn_status: "Published"
learn_rel_path: "Collecting Metrics/DNS and DHCP Servers"
most_popular: False
message: "DO NOT EDIT THIS FILE DIRECTLY, IT IS GENERATED BY THE COLLECTOR'S metadata.yaml FILE"
endmeta-->

# Dnsmasq


<img src="https://khulnasoft.com/img/dnsmasq.svg" width="150"/>


Plugin: go.d.plugin
Module: dnsmasq

<img src="https://img.shields.io/badge/maintained%20by-Khulnasoft-%2300ab44" />

## Overview

This collector monitors Dnsmasq servers.




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



### Per Dnsmasq instance

The metrics apply to the entire monitored application.

This scope has no labels.

Metrics:

| Metric | Dimensions | Unit |
|:------|:----------|:----|
| dnsmasq.servers_queries | success, failed | queries/s |
| dnsmasq.cache_performance | hist, misses | events/s |
| dnsmasq.cache_operations | insertions, evictions | operations/s |
| dnsmasq.cache_size | size | entries |



## Alerts

There are no alerts configured by default for this integration.


## Setup

### Prerequisites

No action required.

### Configuration

#### File

The configuration file name for this integration is `go.d/dnsmasq.conf`.


You can edit the configuration file using the `edit-config` script from the
Khulnasoft [config directory](https://github.com/khulnasoft/khulnasoft/blob/master/docs/khulnasoft-agent/configuration.md#the-khulnasoft-config-directory).

```bash
cd /etc/khulnasoft 2>/dev/null || cd /opt/khulnasoft/etc/khulnasoft
sudo ./edit-config go.d/dnsmasq.conf
```
#### Options

The following options can be defined globally: update_every, autodetection_retry.


<details><summary>Config options</summary>

| Name | Description | Default | Required |
|:----|:-----------|:-------|:--------:|
| update_every | Data collection frequency. | 1 | no |
| autodetection_retry | Recheck interval in seconds. Zero means no recheck will be scheduled. | 0 | no |
| address | Server address in `ip:port` format. | 127.0.0.1:53 | yes |
| protocol | DNS query transport protocol. Supported protocols: udp, tcp, tcp-tls. | udp | no |
| timeout | DNS query timeout (dial, write and read) in seconds. | 1 | no |

</details>

#### Examples

##### Basic

An example configuration.

<details><summary>Config</summary>

```yaml
jobs:
  - name: local
    address: 127.0.0.1:53

```
</details>

##### Using TCP protocol

Local server with specific DNS query transport protocol.

<details><summary>Config</summary>

```yaml
jobs:
  - name: local
    address: 127.0.0.1:53
    protocol: tcp

```
</details>

##### Multi-instance

> **Note**: When you define multiple jobs, their names must be unique.

Collecting metrics from local and remote instances.


<details><summary>Config</summary>

```yaml
jobs:
  - name: local
    address: 127.0.0.1:53

  - name: remote
    address: 203.0.113.0:53

```
</details>



## Troubleshooting

### Debug Mode

To troubleshoot issues with the `dnsmasq` collector, run the `go.d.plugin` with the debug option enabled. The output
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
  ./go.d.plugin -d -m dnsmasq
  ```


