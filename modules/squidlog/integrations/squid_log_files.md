<!--startmeta
custom_edit_url: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/squidlog/README.md"
meta_yaml: "https://github.com/khulnasoft/go.d.plugin/edit/master/modules/squidlog/metadata.yaml"
sidebar_label: "Squid log files"
learn_status: "Published"
learn_rel_path: "Collecting Metrics/Web Servers and Web Proxies"
most_popular: True
message: "DO NOT EDIT THIS FILE DIRECTLY, IT IS GENERATED BY THE COLLECTOR'S metadata.yaml FILE"
endmeta-->

# Squid log files


<img src="https://khulnasoft.com/img/squid.png" width="150"/>


Plugin: go.d.plugin
Module: squidlog

<img src="https://img.shields.io/badge/maintained%20by-Khulnasoft-%2300ab44" />

## Overview

his collector monitors Squid servers by parsing their access log files.


It automatically detects log files of Squid severs running on localhost.


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



### Per Squid log files instance

These metrics refer to the entire monitored application.

This scope has no labels.

Metrics:

| Metric | Dimensions | Unit |
|:------|:----------|:----|
| squidlog.requests | requests | requests/s |
| squidlog.excluded_requests | unmatched | requests/s |
| squidlog.type_requests | success, bad, redirect, error | requests/s |
| squidlog.http_status_code_class_responses | 1xx, 2xx, 3xx, 4xx, 5xx | responses/s |
| squidlog.http_status_code_responses | a dimension per HTTP response code | responses/s |
| squidlog.bandwidth | sent | kilobits/s |
| squidlog.response_time | min, max, avg | milliseconds |
| squidlog.uniq_clients | clients | clients |
| squidlog.cache_result_code_requests | a dimension per cache result code | requests/s |
| squidlog.cache_result_code_transport_tag_requests | a dimension per cache result delivery transport tag | requests/s |
| squidlog.cache_result_code_handling_tag_requests | a dimension per cache result handling tag | requests/s |
| squidlog.cache_code_object_tag_requests | a dimension per cache result produced object tag | requests/s |
| squidlog.cache_code_load_source_tag_requests | a dimension per cache result load source tag | requests/s |
| squidlog.cache_code_error_tag_requests | a dimension per cache result error tag | requests/s |
| squidlog.http_method_requests | a dimension per HTTP method | requests/s |
| squidlog.mime_type_requests | a dimension per MIME type | requests/s |
| squidlog.hier_code_requests | a dimension per hierarchy code | requests/s |
| squidlog.server_address_forwarded_requests | a dimension per server address | requests/s |



## Alerts

There are no alerts configured by default for this integration.


## Setup

### Prerequisites

No action required.

### Configuration

#### File

The configuration file name for this integration is `go.d/squidlog.conf`.


You can edit the configuration file using the `edit-config` script from the
Khulnasoft [config directory](https://github.com/khulnasoft/khulnasoft/blob/master/docs/khulnasoft-agent/configuration.md#the-khulnasoft-config-directory).

```bash
cd /etc/khulnasoft 2>/dev/null || cd /opt/khulnasoft/etc/khulnasoft
sudo ./edit-config go.d/squidlog.conf
```
#### Options

Squid [log format codes](http://www.squid-cache.org/Doc/config/logformat/).

Squidlog is aware how to parse and interpret the following codes:

| field          | squid format code | description                                                   |
|----------------|-------------------|---------------------------------------------------------------|
| resp_time      | %tr               | Response time (milliseconds).                                 |
| client_address | %>a               | Client source IP address.                                     |
| client_address | %>A               | Client FQDN.                                                  |
| cache_code     | %Ss               | Squid request status (TCP_MISS etc).                          |
| http_code      | %>Hs              | The HTTP response status code from Content Gateway to client. |
| resp_size      | %<st              | Total size of reply sent to client (after adaptation).        |
| req_method     | %rm               | Request method (GET/POST etc).                                |
| hier_code      | %Sh               | Squid hierarchy status (DEFAULT_PARENT etc).                  |
| server_address | %<a               | Server IP address of the last server or peer connection.      |
| server_address | %<A               | Server FQDN or peer name.                                     |
| mime_type      | %mt               | MIME content type.                                            |

In addition, to make `Squid` [native log format](https://wiki.squid-cache.org/Features/LogFormat#Squid_native_access.log_format_in_detail) csv parsable, squidlog understands these groups of codes:

| field       | squid format code | description                        |
|-------------|-------------------|------------------------------------|
| result_code | %Ss/%>Hs          | Cache code and http code.          |
| hierarchy   | %Sh/%<a           | Hierarchy code and server address. |


<details><summary>Config options</summary>

| Name | Description | Default | Required |
|:----|:-----------|:-------|:--------:|
| update_every | Data collection frequency. | 1 | no |
| autodetection_retry | Recheck interval in seconds. Zero means no recheck will be scheduled. | 0 | no |
| path | Path to the Squid access log file. | /var/log/squid/access.log | yes |
| exclude_path | Path to exclude. | *.gz | no |
| parser | Log parser configuration. |  | no |
| parser.log_type | Log parser type. | auto | no |
| parser.csv_config | CSV log parser config. |  | no |
| parser.csv_config.delimiter | CSV field delimiter. | space | no |
| parser.csv_config.format | CSV log format. | - $resp_time $client_address $result_code $resp_size $req_method - - $hierarchy $mime_type | yes |
| parser.ltsv_config | LTSV log parser config. |  | no |
| parser.ltsv_config.field_delimiter | LTSV field delimiter. | \t | no |
| parser.ltsv_config.value_delimiter | LTSV value delimiter. | : | no |
| parser.ltsv_config.mapping | LTSV fields mapping to **known fields**. |  | yes |
| parser.regexp_config | RegExp log parser config. |  | no |
| parser.regexp_config.pattern | RegExp pattern with named groups. |  | yes |

##### parser.log_type

Weblog supports 3 different log parsers:

| Parser type | Description                               |
|-------------|-------------------------------------------|
| csv         | A comma-separated values                  |
| ltsv        | [LTSV](http://ltsv.org/)                  |
| regexp      | Regular expression with named groups      |

Syntax:

```yaml
parser:
  log_type: csv
```


##### parser.csv_config.format



##### parser.ltsv_config.mapping

The mapping is a dictionary where the key is a field, as in logs, and the value is the corresponding **known field**.

> **Note**: don't use `$` and `%` prefixes for mapped field names.

```yaml
parser:
  log_type: ltsv
  ltsv_config:
    mapping:
      label1: field1
      label2: field2
```


##### parser.regexp_config.pattern

Use pattern with subexpressions names. These names should be **known fields**.

> **Note**: don't use `$` and `%` prefixes for mapped field names.

Syntax:

```yaml
parser:
  log_type: regexp
  regexp_config:
    pattern: PATTERN
```


</details>

#### Examples
There are no configuration examples.



## Troubleshooting

### Debug Mode

To troubleshoot issues with the `squidlog` collector, run the `go.d.plugin` with the debug option enabled. The output
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
  ./go.d.plugin -d -m squidlog
  ```


