---
layout: page
title: "Customizing entities"
description: "Simple customization for entities in the frontend."
date: 2016-04-20 06:00
sidebar: true
comments: false
sharing: true
footer: true
redirect_from: /getting-started/customizing-devices/
---

By default, all of your devices will be visible and have a default icon determined by their domain. You can customize the look and feel of your front page by altering some of these parameters. This can be done by overriding attributes of specific entities.

```yaml
homeassistant:
  name: Home
  unit_system: metric
  # etc

  customize:
    # Add an entry for each entity that you want to overwrite.
    sensor.living_room_motion:
      hidden: true
    thermostat.family_room:
      entity_picture: https://example.com/images/nest.jpg
      friendly_name: Nest
    switch.wemo_switch_1:
      friendly_name: Toaster
      entity_picture: /local/toaster.jpg
    switch.wemo_switch_2:
      friendly_name: Kitchen kettle
      icon: mdi:kettle
    switch.rfxtrx_switch:
      assumed_state: false
  # Customize all entities in a domain
  customize_domain:
    light:
      icon: mdi:home
  # Customize entities matching a pattern
  customize_glob:
    "light.kitchen_*":
      icon: mdi:description

```

### {% linkable_title Possible values %}

| Attribute | Description |
| --------- | ----------- |
| `friendly_name` | Name of the entity
| `hidden`    | Set to `true` to hide the entity.
| `entity_picture` | Url to use as picture for entity
| `icon` | Any icon from [MaterialDesignIcons.com](http://MaterialDesignIcons.com). Prefix name with `mdi:`, ie `mdi:home`.
| `assumed_state` | For switches with an assumed state two buttons are shown (turn off, turn on) instead of a switch. By setting `assumed_state` to `false` you will get the default switch icon.
| `device_class` | Sets the class of the device, changing the device state and icon that is displayed on the UI (see below).

### {% linkable_title Device Class %}

Device class is currently supported by the following platforms:

* [Binary Sensor](/components/binary_sensor/)
* [Cover](/components/cover/)

### {% linkable_title Reloading customize %}

Home Assistant offers a service to reload the core configuration while Home Assistant is running called `homeassistant/reload_core_config`. This allows you to change your customize section and see it being applied without having to restart Home Assistant. To call this service, go to the <img src='/images/screenshots/developer-tool-services-icon.png' alt='service developer tool icon' class="no-shadow" height="38" /> service developer tools, select the service `homeassistant/reload_core_config` and click "Call Service".

<p class='note warning'>
New customize information will be applied the next time the state of the entity gets updated.
</p>

