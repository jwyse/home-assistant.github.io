---
layout: page
title: "Check Home Assistant configuration"
description: "Check Home Assistant configuration against a new version"
date: 2017-04-30 13:28
sidebar: true
comments: false
sharing: true
footer: true
---

You can use this addon to check whether your configuration files are valid against the new version of Home Assistant before you actually update your Home Assistant. This will help you avoid errors due to breaking changes, resulting in smooth update.

```json
{
  "version": "latest"
}
```

Configuration variables:

- **version** (*Required*): Version of Home Assistant that you plan to install.
