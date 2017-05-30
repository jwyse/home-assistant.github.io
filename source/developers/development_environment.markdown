---
layout: page
title: "Set up Development Environment"
description: "Set up your environment to start developing for Home Assistant."
date: 2014-12-21 13:32
sidebar: true
comments: false
sharing: true
footer: true
---

You'll need to set up a development environment if you want to develop a new feature or component for Home Assistant. Read on to learn how to set up.

### {% linkable_title Preparing your environment %}

#### {% linkable_title Developing on Linux %}

Install the core dependencies.
```bash
$ sudo apt-get install python3-pip python3-dev python3-venv
```

In order to run `script/setup` below you will need some more dependencies.
```bash
$ sudo apt-get install libssl-dev libxml2-dev libxslt1-dev libjpeg-dev libffi-dev libudev-dev
```

<p class='note'>
Different distributions have different package installation mechanisms and sometimes packages names as well. For example Centos would use: `sudo yum install epel-release && sudo yum install python34 python34-devel mysql-devel`
</p>

Additional dependencies exist if you you plan to perform Frontend Development, please read the [Frontend](https://home-assistant.io/developers/frontend/) section to learn more.

#### {% linkable_title Developing on Windows %}

If you are using Windows as a development platform, make sure that you have the correct Microsoft Visual C++ build tools installed. Check the [Windows Compilers](https://wiki.python.org/moin/WindowsCompilers) section on the [Python website](https://www.python.org/) for details. Validation using `tox` will fail if this is not done correctly.

Also, make sure to install or upgrade the `setuptools` Python package. It contains compatibility improvements and adds automatic use of compilers:

```bash
$ pip install --upgrade setuptools
```

#### {% linkable_title Developing on OS X %}

Install [Homebrew](https://brew.sh/), then use that to install Python 3:

```bash
$ brew install python3
```

### {% linkable_title Setup Local Repository %}

Visit the [Home Assistant repository](https://github.com/home-assistant/home-assistant) and click **Fork**.
Once forked, setup your local copy of the source using the commands:

```bash
$ git clone https://github.com/YOUR_GIT_USERNAME/home-assistant.git
$ cd home-assistant
$ git remote add upstream https://github.com/home-assistant/home-assistant.git
```

### {% linkable_title Setting up virtual environment (optional) %} 

If you plan on providing isolation to your environment using [`venv`](https://docs.python.org/3.4/library/venv.html). Within the `home-assistant` directory, create and activate your virtual environment.

```bash
$ python3 -m venv venv
$ source venv/bin/activate
```

### {% linkable_title Setup and Run %}

```bash
$ cd home-assistant
$ script/setup
```

* Run `hass` to invoke your local installation.

### {% linkable_title Logging %}

By default logging in home-assistant is tuned for operating in
production (set to INFO by default, with some modules set to even less
verbose logging levels).

You can use the [logger](/components/logger/) component to adjust
logging to DEBUG to see even more details about what is going on.
