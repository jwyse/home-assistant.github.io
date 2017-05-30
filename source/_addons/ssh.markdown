---
layout: page
title: "SSH Server"
description: "Allow logging in remotely to your server using SSH."
date: 2017-04-30 13:28
sidebar: true
comments: false
sharing: true
footer: true
---

Setting up an [SSH](https://openssh.org/) server allows access to your Hass.io folders with any SSH client. To use this add-on, you must have a private/public key to log in. To generate them, follow the [instructions for Windows][win] and [these for other platforms][other].

```json
{
  "authorized_keys": [
    "ssh-rsa AKDJD3839...== my-key"
  ]
}
```

Configuration variables:

- **authorized_keys** (*Required*): Your public-keys for authorized keyfile. Every element will be a line inside that file.

[win]: https://www.digitalocean.com/community/tutorials/how-to-create-ssh-keys-with-putty-to-connect-to-a-vps
[other]: https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

<p class='note'>
This add-on is not compatible when you installed Hass.io via the generic Linux installer.
</p>
