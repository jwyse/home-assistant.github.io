---
layout: page
title: "Seven segments display"
description: "Instructions how to use OCR for seven segemnts displays into Home Assistant."
date: 2017-05-18 08:00
sidebar: true
comments: false
sharing: true
footer: true
logo: home-assistant.png
ha_category: Image Processing
featured: false
ha_release: 0.45
og_image: /images/screenshots/ssocr.png
---

The `seven_segments` image processing platform allows you to read physical seven segments displays through Home Assistant. [`ssocr`](https://www.unix-ag.uni-kl.de/~auerswal/ssocr/) is used to extract the value shown on the display which is observed by a [camera](/components/camera/). `ssocr` need to be available on your system. Check the installation instruction for Fedora below or use `$ sudo apt-get install ssocr` on a Debian-based system:

```bash
$ sudo dnf -y install imlib2-devel
$ git clone https://github.com/auerswal/ssocr.git
$ cd ssocr
$ make
$ sudo make PREFIX=/usr install
```

To enable the OCR of a seven segement display in your installation, add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
image_processing:
  - platform: seven_segments
    source:
      - entity_id: camera.seven_segments
```

Configuration variables:

- **ssocr_bin** (*Optional*): The command line tool `ssocr`. Set it if you use a different name for the executable. Defaults to `ssocr`.
- **x_position** (*Optional*): X coordinate of the upper left corner of the area to crop. Defaults to `0`.
- **y_position** (*Optional*):  Y coordinate of the upper left corner of the area to crop. Defaults to `0`.
- **height** (*Optional*): Height of the area to crop. Defaults to `0`.
- **width** (*Optional*): Width of the area to crop. Defaults to `0`.
- **threshold** (*Optional*): Threshold for the difference between the digits and the background. Defaults to `0`.
- **digits** (*Optional*): Number of digits in the display. Defaults to `-1`.
- **source** array (*Required*): List of image sources.
  - **entity_id** (*Required*): A camera entity id to get picture from.
  - **name** (*Optional*): This parameter allows you to override the name of your `image_processing` entity.


### {% linkable_title Setup process %}

It's suggested that the first attempt to determine the needed parameters is using `ssocr` directly. This may require a couple of iterations to get the result

```bash
$ ssocr -D erosion crop 390 250 490 280 -t 20 -d 4 ss-test.jpg
```

This would lead to the following entry for the `configuration.yaml` file:

```yaml
camera:
  - platform: local_file
    file_path: /home/fab/.homeassistant/seven-seg.png
    name: seven_segments
image_processing:
  - platform: seven_segments
    x_position: 390
    y_position: 250
    height: 280
    width: 490
    threshold: 20
    digits: 4
    source:
      - entity_id: camera.seven_segments
```

<p class='img'>
  <img src='{{site_root}}/images/screenshots/ssocr.png' />
</p>

With the help of a [template sensor](/components/sensor.template/), the value can be shown as badge.

```yaml
sensor:
  - platform: template
    sensors:
      power_meter:
        value_template: '{{ states.image_processing.sevensegement_ocr_seven_segments.state }}'
        friendly_name: 'Ampere'
        unit_of_measurement: 'A'
```

