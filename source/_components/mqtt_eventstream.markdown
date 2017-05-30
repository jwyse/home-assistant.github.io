---
layout: page
title: "MQTT Eventstream"
description: "Instructions how to setup MQTT eventstream within Home Assistant."
date: 2016-01-13 08:00
sidebar: true
comments: false
sharing: true
footer: true
logo: mqtt.png
ha_category: Other
ha_release: 0.11
---

The `mqtt_eventstream` component connects two Home Assistant instances via MQTT.

To integrate MQTT Eventstream into Home Assistant, add the following section to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
mqtt_eventstream:
  publish_topic: MyServerName
  subscribe_topic: OtherHaServerName
```

Configuration variables:

- **publish_topic** (*Optional*): Topic for publishing local events
- **subscribe_topic** (*Optional*): Topic to receive events from the remote server.

## Multiple Instances

Events from multiple instances can be aggregated to a single master instance by subscribing to a wildcard topic from the master instance.

```yaml
# Example master instance configuration.yaml entry
mqtt_eventstream:
  publish_topic: master/topic
  subscribe_topic: slaves/#
```

For a multiple instance setup, each slave would publish to their own topic.

```yaml
# Example slave instance configuration.yaml entry
mqtt_eventstream:
  publish_topic: slaves/upstairs
  subscribe_topic: master/topic
```

```yaml
# Example slave instance configuration.yaml entry
mqtt_eventstream:
  publish_topic: slaves/downstairs
  subscribe_topic: master/topic
```
