<!--startmeta
custom_edit_url: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/logind/README.md"
meta_yaml: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/logind/metadata.yaml"
sidebar_label: "systemd-logind users"
learn_status: "Published"
learn_rel_path: "Collecting Metrics/Systemd"
most_popular: False
message: "DO NOT EDIT THIS FILE DIRECTLY, IT IS GENERATED BY THE COLLECTOR'S metadata.yaml FILE"
endmeta-->

# systemd-logind users


<img src="https://khulnasoft.com/img/users.svg" width="150"/>


Plugin: go.d.plugin
Module: logind

<img src="https://img.shields.io/badge/maintained%20by-Khulnasoft-%2300ab44" />

## Overview

This collector monitors number of sessions and users as reported by the `org.freedesktop.login1` DBus API.




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



### Per systemd-logind users instance

These metrics refer to the entire monitored application.

This scope has no labels.

Metrics:

| Metric | Dimensions | Unit |
|:------|:----------|:----|
| logind.sessions | remote, local | sessions |
| logind.sessions_type | console, graphical, other | sessions |
| logind.sessions_state | online, closing, active | sessions |
| logind.users_state | offline, closing, online, lingering, active | users |



## Alerts

There are no alerts configured by default for this integration.


## Setup

### Prerequisites

No action required.

### Configuration

#### File

The configuration file name for this integration is `go.d/logind.conf`.


You can edit the configuration file using the `edit-config` script from the
Khulnasoft [config directory](https://github.com/khulnasoft/khulnasoft/blob/master/docs/khulnasoft-agent/configuration.md#the-khulnasoft-config-directory).

```bash
cd /etc/khulnasoft 2>/dev/null || cd /opt/khulnasoft/etc/khulnasoft
sudo ./edit-config go.d/logind.conf
```
#### Options

The following options can be defined globally: update_every, autodetection_retry.


#### Examples
There are no configuration examples.



## Troubleshooting

### Debug Mode

To troubleshoot issues with the `logind` collector, run the `go.d.plugin` with the debug option enabled. The output
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
  ./go.d.plugin -d -m logind
  ```


