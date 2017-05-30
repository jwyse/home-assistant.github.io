---
layout: page
title: "Installation on Docker"
description: "Instructions to install Home Assistant on a Docker."
date: 2016-04-16 11:36
sidebar: true
comments: false
sharing: true
footer: true
redirect_from: /getting-started/installation-docker/
---

Installation with Docker is straightforward. Adjust the following command so that `/path/to/your/config/` points at the folder where you want to store your config and run it:

### {% linkable_title Linux %}

```bash
$ docker run -d --name="home-assistant" -v /path/to/your/config:/config -v /etc/localtime:/etc/localtime:ro --net=host homeassistant/home-assistant
```

### {% linkable_title macOS %}

When using `boot2docker` on macOS you are unable to map the local time to your Docker container. Use `-e "TZ=America/Los_Angeles"` instead of `-v /etc/localtime:/etc/localtime:ro`. Replace "America/Los_Angeles" with [your timezone](http://en.wikipedia.org/wiki/List_of_tz_database_time_zones).

Additionally, if your expectation is that you will be able to browse directly to `http://localhost:8123` on your macOS host, then you will also need to replace the `--net=host` switch with `-p 8123:8123`. This is currently the only way to forward ports on to your actual host (macOS) machine instead of the virtual machine inside `xhyve`. More detail on this can be found in [the docker forums](https://forums.docker.com/t/should-docker-run-net-host-work/14215/10).

```bash
$ docker run -d --name="home-assistant" -v /path/to/your/config:/config -e "TZ=America/Los_Angeles" -p 8123:8123 homeassistant/home-assistant
```

### {% linkable_title Windows %}

When running Home Assistant in Docker on Windows, you may have some difficulty getting ports to map for routing (since the `--net=host` switch actually applies to the hypervisor's network interface). To get around this, you will need to add port proxy ipv4 rules to your local Windows machine, like so (Replacing '192.168.1.10' with whatever your Windows IP is, and '10.0.50.2' with whatever your Docker container's IP is):
```
netsh interface portproxy add v4tov4 listenaddress=192.168.1.10 listenport=8123 connectaddress=10.0.50.2 connectport=8123
netsh interface portproxy add v4tov4 listenaddress=0.0.0.0 listenport=8123 connectaddress=10.0.50.2 connectport=8123
```

This will let you access your Home Assistant portal from http://localhost:8123, and if you forward port 8123 on your router to your machine IP, the traffic will be forwarded on through to the docker container.

### {% linkable_title Synology NAS %}

As Synology within DSM now supports Docker (with a neat UI), you can simply install Home Assistant using docker without the need for command-line. For details about the package (including compatability-information, if your NAS is supported), see https://www.synology.com/en-us/dsm/app_packages/Docker

The steps would be:
* Install "Docker" package on your Synology NAS
* Launch Docker-app and move to "Registry"-section
* Find "homeassistant/home-assistant" with registry and click on "Download"
* Wait for some time until your NAS has pulled the image
* Move to the "Image"-section of the Docker-app
* Click on "Launch"
* Choose a container-name you want (e.g. "homeassistant")
* Click on "Advanced Settings"
* Set "Enable auto-restart" if you like
* Within "Volume" click on "Add Folder" and choose either an existing folder or add a new folder. The "mount point" has to be "/config", so that Home Assistant will use it for the configs and logs.
* Within "Network" select "Use same network as Docker Host"
* Confirm the "Advanced Settings"
* Click on "Next" and then "Apply"
* Your Home Assistant within Docker should now run

Remark: to update your Home Assistant on your Docker within Synology NAS, you just have to do the following:
* Go to the Docker-app and move to "Image"-section
* Download the "homeassistant/home-assistant" image - don't care, that it is already there
* wait until the system-message/-notification comes up, that the download is finished (there is no progress bar)
* Move to "Container"-section
* Stop your container if it's running
* Right-click on it and select "Action"->"Clear". You won't loose any data, as all files are stored in your config-directory
* Start the container again - it will then boot up with the new Home Assistant image

### {% linkable_title Restart %}

This will launch Home Assistant and serve the web interface from port 8123 on your Docker host.

If you change the configuration you have to restart the server. To do that you have 2 options.

 1. You can go to the <img src='/images/screenshots/developer-tool-services-icon.png' alt='service developer tool icon' class="no-shadow" height="38" /> service developer tools, select the service `homeassistant/restart` and click "Call Service".
 2. Or you can restart it from an terminal by running `docker restart home-assistant`
