---
title: SignalFx Plugin
brief: SignalFx plugin to configure write-http to send metrics from collectd.
---

# SignalFx collectd Plugin

_This is a directory consolidate all the metadata associated with the SignalFx collectd plugin. The relevant code for the plugin can be found [here](https://github.com/signalfx/collectd-signalfx/)_

- [Description](#description)
- [Requirements and Dependencies](#requirements-and-dependencies)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Metrics](#metrics)
- [License](#license)

### DESCRIPTION

This SignalFx metadata plugin for collectd configures collectd to aggregate metrics and send then to SignalFx. This plugin also handles the association to a specific SignalFx org to the data that is being sent through the org's API token.

### REQUIREMENTS AND DEPENDENCIES

This plugin requires:

| Software          | Version        |
|-------------------|----------------|
| collectd  |  4.9+  |
| Python plugin for collectd | (included with SignalFx collectd) |
| Python    |  2.6+ |

### INSTALLATION

1. Install the Python plugin for collectd.

 ##### RHEL/CentOS 6.x & 7.x, and Amazon Linux 2014.09, 2015.03 & 2015.09

 Run the following command to install the Python plugin for collectd:
 ```
 yum install collectd-python
 ```
 ##### Ubuntu 12.04, 14.04, 15.04 & Debian 7, 8:

 This plugin is included with [SignalFx's collectd package](https://support.signalfx.com/hc/en-us/articles/208080123).

1. Download the Python module from the following URL:

 https://github.com/signalfx/signalfx-collectd-plugin

1. Download SignalFx’s [sample configuration file](https://github.com/signalfx/integrations/blob/master/collectd-signalfx/10-signalfx.conf).

1. Modify the configuration file as follows:

 1. Modify the fields “TypesDB and “ModulePath” to point to the location on disk where you downloaded the Python module in step 2.

 1. Provide values that make sense for your environment, as described [below](#configuration).

1. Add the following line to /etc/collectd.conf, replacing the example path with the location of the configuration file you downloaded in step 4:
 ```
 include '/path/to/10-signalfx.conf'
 ```
1. Restart collectd.

collectd will begin emitting metrics to SignalFx.

### CONFIGURATION

You will need to add your API Token to allow the metric data to be sent to the SignalFx service.

Directions for finding your token:
1. Open your SignalFx profile page at https://app.signalfx.com/#/myprofile.
1. Locate the words "API Token" on the page.
1. Click the link next to "API Token" that says "show". Your API token appears.
1. Copy the value of the token to the "Token" field in this config.

| configuration option | definition | default value |
| ---------------------|------------|---------------|
| ModulePath | Path on disk where collectd can find this module. | "/opt/signalfx-collectd-plugin" |
| URL | URL for where metrics are sent from collectd. If you are looking to limit the number of connections from your infrastructure to the SignalFx service you can optioally configure the use of the [SignalFx metricproxy](https://github.com/signalfx/integrations/tree/master/metricproxy) | "https://ingest.signalfx.com/v1/collectd" |
| Token | API token for your SignalFx org | none |
| LogTraces | Enable log traces | true |
| Notifications | Enable notification on this plugin | true |
| NotifyLevel | Set the notification level | "OKAY" |


### USAGE

This plugin provides additional aggregated system metrics to SignalFx.

### METRICS

For documentation of the metrics and dimensions emitted by this plugin, [click here](././docs).

### LICENSE

This plugin is released under the Apache 2.0 license. See [LICENSE](https://github.com/signalfx/signalfx-collectd-plugin/blob/master/LICENSE) for more details.
