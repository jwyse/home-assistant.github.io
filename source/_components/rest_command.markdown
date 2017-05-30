---
layout: page
title: "RESTful Command"
description: "Instructions how to integrate REST commands into Home Assistant."
date: 2016-12-27 00:00
sidebar: true
comments: false
sharing: true
footer: true
logo: restful.png
ha_category: Automation
ha_release: 0.36
---

This component can expose regular REST commands as services. Services can be called from a [script] or in [automation].

[script]: /components/script/
[automation]: /getting-started/automation/

To enable this switch, add the following lines to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
rest_command:
  example_request:
    url: 'http://example.com/'
```

Configuration variables:

- **[service_name]** (*Required*): The name used to expose the service. E.g. in the above example would it be ` rest_command.example_request`.
  - **url** (*Required*): The URL (support template) for sending request.
  - **method** (*Optional*): HTTP method (get, post, put, delete). Default is get.
  - **payload** (*Optional*): A string/template to send with request.
  - **username** (*Optional*): The username for HTTP authentication.
  - **password** (*Optional*): The password for HTTP authentication.
  - **timeout** (*Optional*): Timeout for requests. Defaults to 10 seconds.
  - **content_type** (*Optional*): Content type for the request.

The commands can be dynamic, using templates to insert values of other entities. Service call support variables for template stuff.

