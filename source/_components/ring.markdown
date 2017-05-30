---
layout: page
title: "Ring"
description: "Instructions on how to integrate your Ring.com devices within Home Assistant."
date: 2017-04-01 10:00
sidebar: true
comments: false
sharing: true
footer: true
logo: ring.png
ha_category: Hub
ha_release: 0.42
---

The `ring` implementation allows you to integrate your [Ring.com](https://ring.com/) devices in Home Assistant.

Currently only doorbells are supported by this sensor.

To enable device linked in your [Ring.com](https://ring.com/) account, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
ring:
  username: you@example.com
  password: secret
```

Configuration variables:

- **username** (*Required*): The username for accessing your Ring account.
- **password** (*Required*): The password for accessing your Ring account.

Finish its configuration by visiting the [Ring binary_sensor page](/components/binary_sensor.ring/) or [Ring sensor page](/components/sensor.ring/).
