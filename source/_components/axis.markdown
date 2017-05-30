---
layout: page
title: "Axis"
description: "Instructions on how to setup devices from Axis Communications within Home Assistant."
date: 2017-04-30 23:04
sidebar: true
comments: false
sharing: true
footer: true
logo: axis.png
ha_category: Hub
ha_release: "0.45"
---

[Axis Communications](https://www.axis.com/) devices are surveillance cameras and other security related network connected hardware. Sensor API works with firmware 5.50 and newer.

Home Assistant will automatically discover their presence on your network.

You can also manually configure your devices by adding the following lines to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
axis:
  m1065lw:
    host: IP ADDRESS
    username: USERNAME
    password: PASSWORD
    include:
    - camera
    - motion
    - pir
    - sound
    - daynight
    trigger_time: 0
    location: köket
```

## {% linkable_title Dependencies %}

```bash
sudo apt-get install python3-gi gir1.2-gstreamer-1.0
```

Depending on how you run Home Assistant you might be needed to symlink the `gi` module into your environment (e.g. in Hassbian):

```bash
ln -s /usr/lib/python3/dist-packages/gi /srv/homeassistant/lib/python3.4/site-packages
```

## {% linkable_title Configuration variables %}

- **device** (*Required*): Unique name 
- **host** (*Required*): The IP address to your Axis device.
- **username** (*Optional*): The username to your Axis device. Default 'root'.
- **password** (*Optional*): The password to your Axis device. Default 'pass'.
- **trigger_time** (*Optional*): Minimum time (in seconds) a sensor should keep its positive value. Default 0.
- **location** (*Optional*): Physical location of your Axis device. Default not set.

- **include** (*Required*): This cannot be empty else there would be no use adding the device at all.
  - **camera**: Stream MJPEG video to Home Assistant
  - **motion**: The Built in motion detection in Axis cameras
  - **vmd3**: ACAP Motion Detection app which has better algorithms for motion detection
  - **pir**: PIR sensor that can trigger on motion
  - **sound**: Sound detector
  - **daynight**: Certain cameras have day/night mode if they have built-in IR lights
  - **tampering**: signals when camera believes that it has been tampered with
  - **input**: trigger on whatever you have connected to device input port

<p class='note'>
Any specific levels for triggers needs to be configured on the device.
</p>

<p class='note'>
  It is recommended that you create a user on your Axis device specifically for Home Assistant. For all current functionality it is enough to create a user belonging to user group viewer.
</p>
