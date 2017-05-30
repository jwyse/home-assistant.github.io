---
layout: page
title: "Add-On Configuration"
description: "Steps on how-to create an add-on for Hass.io."
date: 2017-04-30 13:28
sidebar: true
comments: false
sharing: true
footer: true
---

Each add-on is stored in a folder. The file structure looks like this:

```
addon_name/
  Dockerfile
  config.json
  run.sh
```

## {% linkable_title Add-on script %}

As with every Docker container, you will need a script to run when the container is started. A user might run many add-ons, so it is encouraged to try to stick to Bash scripts if you're doing simple things.

When developing your script:

 - `/data` is a volume for persistent storage.
 - `/data/options.json` contains the user configuration. You can use `jq` inside your shell script to parse this data.

```bash
echo '{ "target": "beer" }' | jq -r ".target"
```

## {% linkable_title Add-on Docker file %}

All add-ons are based on Alpine Linux 3.5. Hass.io will automatically substitute the right base image based on the machine architecture. Add `tzdata` if you need run in correct timezone.

```
FROM %%BASE_IMAGE%%

ENV LANG C.UTF-8

# Install requirements for add-on
RUN apk add --no-cache tzdata jq

# Copy data for add-on
COPY run.sh /
RUN chmod a+x /run.sh

CMD [ "/run.sh" ]
```

If you don't use local build on device or our build script, make sure that the Dockerfile have also a set of labels include:
```
LABEL io.hass.version="VERSION" io.hass.type="addon" io.hass.arch="armhf|aarch64|i386|amd64"
```

## {% linkable_title Add-on config %}

The config for an add-on is stored in `config.json`.

```json
{
  "name": "xy",
  "version": "1.2",
  "slug": "folder",
  "description": "long descripton",
  "arch": ["amd64"],
  "url": "website with more information about add-on (ie a forum thread for support)",
  "startup": "before",
  "boot": "auto",
  "ports": {
    "123/tcp": 123
  },
  "map": ["config:rw", "ssl"],
  "options": {},
  "schema": {},
  "image": "repo/{arch}-my-custom-addon"
}
```

| Key | Required | Description |
| --- | -------- | ----------- |
| name | yes | Name of the add-on
| version | yes | Version of the add-on
| slug | yes | Slug of the add-on
| description | yes | Description of the add-on
| arch | no | List of supported arch: `armhf`, `aarch64`, `amd64`, `i386`. Default all.
| url | no | Homepage of the addon. Here you can explain the add-ons and options.
| startup | yes | `initialize` will start addon on setup of hassio. `before` homeassistant will start. `after` homeassistant will start or `once` for application they don't run as deamon.
| boot | yes | `auto` by system and manual or only `manual`
| ports | no | Network ports to expose from the container. Format is `"container-port/type": host-port`.
| host_network | no | If that is True, the add-on run on host network.
| devices | no | Device list to map into add-on. Format is: `<path_on_host>:<path_in_container>:<cgroup_permissions>`
| map | no | List of maps for additional hass.io folders. Possible values: `config`, `ssl`, `addons`, `backup`, `share`. Default it map it `ro`, you can change that if you add a ":rw" at the end of name.
| environment | no | A dict of environment variable to run add-on.
| options | yes | Default options value of the add-on
| schema | yes | Schema for options value of the add-on
| image | no | For use dockerhub.

### {% linkable_title Options / Schema %}

The `options` dict contains all available options and their default value. Set the default value to `null` if the value is required to be given by the user before the add-on can start. Only non-nested arrays are supported.

```json
{
  "message": "custom things",
  "logins": [
    { "username": "beer", "password": "123456" },
    { "username": "cheep", "password": "654321" }
  ],
  "random": ["haha", "hihi", "huhu", "hghg"],
  "link": "http://blebla.com/"
}
```

The `schema` looks like `options` but describes how we should validate the user input. For example:

```json
{
  "message": "str",
  "logins": [
    { "username": "str", "password": "str" }
  ],
  "random": ["str"],
  "link": "url"
}
```

We support:
- str
- bool
- int
- float
- email
- url
