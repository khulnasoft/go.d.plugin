<!--startmeta
custom_edit_url: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/supervisord/README.md"
meta_yaml: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/supervisord/metadata.yaml"
sidebar_label: "Supervisor"
learn_status: "Published"
learn_rel_path: "Collecting Metrics/Processes and System Services"
most_popular: False
message: "DO NOT EDIT THIS FILE DIRECTLY, IT IS GENERATED BY THE COLLECTOR'S metadata.yaml FILE"
endmeta-->

# Supervisor


<img src="https://khulnasoft.com/img/supervisord.png" width="150"/>


Plugin: go.d.plugin
Module: supervisord

<img src="https://img.shields.io/badge/maintained%20by-Khulnasoft-%2300ab44" />

## Overview

This collector monitors Supervisor instances.

It can collect metrics from:

- [unix socket](http://supervisord.org/configuration.html?highlight=unix_http_server#unix-http-server-section-values)
- [internal http server](http://supervisord.org/configuration.html?highlight=unix_http_server#inet-http-server-section-settings)

Used methods:

- [`supervisor.getAllProcessInfo`](http://supervisord.org/api.html#supervisor.rpcinterface.SupervisorNamespaceRPCInterface.getAllProcessInfo)




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



### Per Supervisor instance

These metrics refer to the entire monitored application.

This scope has no labels.

Metrics:

| Metric | Dimensions | Unit |
|:------|:----------|:----|
| supervisord.summary_processes | running, non-running | processes |

### Per process group

These metrics refer to the process group.

This scope has no labels.

Metrics:

| Metric | Dimensions | Unit |
|:------|:----------|:----|
| supervisord.processes | running, non-running | processes |
| supervisord.process_state_code | a dimension per process | code |
| supervisord.process_exit_status | a dimension per process | exit status |
| supervisord.process_uptime | a dimension per process | seconds |
| supervisord.process_downtime | a dimension per process | seconds |



## Alerts

There are no alerts configured by default for this integration.


## Setup

### Prerequisites

No action required.

### Configuration

#### File

The configuration file name for this integration is `go.d/supervisord.conf`.


You can edit the configuration file using the `edit-config` script from the
Khulnasoft [config directory](https://github.com/khulnasoft/khulnasoft/blob/master/docs/khulnasoft-agent/configuration.md#the-khulnasoft-config-directory).

```bash
cd /etc/khulnasoft 2>/dev/null || cd /opt/khulnasoft/etc/khulnasoft
sudo ./edit-config go.d/supervisord.conf
```
#### Options

The following options can be defined globally: update_every, autodetection_retry.


<details><summary>Config options</summary>

| Name | Description | Default | Required |
|:----|:-----------|:-------|:--------:|
| update_every | Data collection frequency. | 1 | no |
| autodetection_retry | Recheck interval in seconds. Zero means no recheck will be scheduled. | 0 | no |
| url | Server URL. | http://127.0.0.1:9001/RPC2 | yes |
| timeout | System bus requests timeout. | 1 | no |

</details>

#### Examples

##### HTTP

Collect metrics via HTTP.

<details><summary>Config</summary>

```yaml
jobs:
  - name: local
    url: 'http://127.0.0.1:9001/RPC2'

```
</details>

##### Socket

Collect metrics via Unix socket.

<details><summary>Config</summary>

```yaml
- name: local
  url: 'unix:///run/supervisor.sock'

```
</details>

##### Multi-instance

> **Note**: When you define multiple jobs, their names must be unique.

Collect metrics from local and remote instances.


<details><summary>Config</summary>

```yaml
jobs:
  - name: local
    url: 'http://127.0.0.1:9001/RPC2'

  - name: remote
    url: 'http://192.0.2.1:9001/RPC2'

```
</details>



## Troubleshooting

### Debug Mode

To troubleshoot issues with the `supervisord` collector, run the `go.d.plugin` with the debug option enabled. The output
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
  ./go.d.plugin -d -m supervisord
  ```


