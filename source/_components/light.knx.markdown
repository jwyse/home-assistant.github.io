---
layout: page
title: "KNX Light"
description: "Instructions on how to integrate KXN lights with Home Assistant."
date: 2016-06-24 12:00
sidebar: true
comments: false
sharing: true
footer: true
logo: knx.png
ha_category: DIY
ha_release: 0.44 
ha_iot_class: "Local Polling"
---


The `knx` light component is used as in interface to switching/light actuators.

To use your KNX light in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
light:
  - platform: knx
    name: KNX light
    address: 0/0/1
```

- **name** (*Optional*): A name for this devices used within Home assistant
- **address** (*Required*): The KNX group address that is used to turn on/off this actuator channel
- **state_address** (*Optional*): Some KNX devices can change their state internally without any messages on the KXN bus, e.g. if you configure a timer on a channel. The optional `state_address` can be used to inform Home Assistant about these state changes. If a KNX message is seen on the bus addressed to the given state address, this will overwrite the state of the switch object.
For switching/light actuators that are only controlled by a single group address and can't change their state internally, you don't have to configure the state address.

