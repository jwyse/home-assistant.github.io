---
layout: page
title: "Amcrest IP Camera"
description: "Instructions how to integrate Amcrest IP cameras within Home Assistant."
date: 2016-11-24 10:00
sidebar: true
comments: false
sharing: true
footer: true
logo: amcrest.png
ha_category: Camera
ha_release: 0.34
---

The `amcrest` platform allows you to integrate your [Amcrest](https://amcrest.com/) IP camera in Home Assistant.

To enable your camera in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
camera:
  - platform: amcrest
    host: IP_ADDRESS
    username: USERNAME
    password: PASSWORD
```

Configuration variables:

- **host** (*Required*): The IP address or hostname of your camera. If using hostname, make sure the DNS works as expected.
- **username** (*Required*): The username for accessing your camera.
- **password** (*Required*): The password for accessing your camera.
- **name** (*Optional*): This parameter allows you to override the name of your camera. The default is "Amcrest Camera".
- **port** (*Optional*): The port that the camera is running on. The default is 80.
- **resolution** (*Optional*): This parameter allows you to specify the camera resolution. For a high resolution (1080/720p), specify the option `high`. For VGA resolution (640x480p), specify the option `low`. If omitted, it defaults to *high*.
- **stream_source** (*Optional*): The data source for the live stream. `mjpeg` will use the camera's native MJPEG stream, whereas `snapshot` will use the camera's snapshot API to create a stream from still images. You can also set the `rtsp` option to generate the streaming via RTSP protocol. If omitted, it defaults to *mjpeg*.
- **ffmpeg_arguments**: (*Optional*): Extra options to pass to ffmpeg, e.g. image quality or video filter options.

**Note:** Amcrest cameras with newer firmwares no longer have the ability to stream `high` definition video with MJPEG encoding. You may need to use `low` resolution stream or the `snapshot` stream source instead.  If the quality seems too poor, lower the `Frame Rate (FPS)` and max out the `Bit Rate` settings in your camera's configuration manager.

**Note:** If you set the `stream_source` option to `rtsp`, make sure to follow the steps mentioned at
[FFMPEG](https://home-assistant.io/components/ffmpeg/) documentation to install the `ffmpeg`.

To check if your Amcrest camera is supported/tested, visit the [supportability matrix](https://github.com/tchellomello/python-amcrest#supportability-matrix) link from the `python-amcrest` project.
