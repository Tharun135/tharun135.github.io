---
title: API Reference: IIH Essentials
description: Technical specifications and endpoints for the Industrial Information Hub.
---

## Overview

Description of the REST API of IIH Essentials.

- **Version**: 2.4.0
- **Connection Timeout**: 10 seconds
- **Max Request Limit**: 16 MB (per single request, non-file)
- **Base Specifications**: Anchor Asset API v1.0

### Target Servers

The API can be accessed via the following endpoints:

| Environment | Base URL |
| :--- | :--- |
| **Local Development** | `http://localhost:4203` |
| **Docker Container** | `http://edgeappdataservice:4203` |
| **Industrial Edge Device** | `https://{ip_or_address_of_ied}/iih-essentials` |

---

## Endpoints: Adapters

### `GET /DataService/Adapters`
**Get all available adapters.**

Retrieves a list of all adapters currently configured in the system.

=== "cURL"
    ```bash
    curl -X 'GET' \
      -H 'Accept: application/json' \
      'http://localhost:4203/DataService/Adapters'
    ```

=== "Python"
    ```python
    import http.client
    
    conn = http.client.HTTPConnection("localhost:4203")
    conn.request("GET", "/DataService/Adapters")
    
    res = conn.getresponse()
    data = res.read()
    print(data.decode("utf-8"))
    ```

=== "JavaScript"
    ```javascript
    const xhr = new XMLHttpRequest();
    xhr.withCredentials = true;

    xhr.addEventListener("readystatechange", function () {
        if (this.readyState === this.DONE) {
            console.log(this.responseText);
        }
    });

    xhr.open("GET", "http://localhost:4203/DataService/Adapters");
    xhr.send(null);
    ```

#### Response (Success)

```json title="application/json"
{
  "adapters": [
    {
      "id": "profinet",
      "name": "Profinet IO Connector",
      "type": "simaticadapter",
      "locked": true,
      "active": true,
      "isDefault": false,
      "canBrowse": true,
      "connected": false,
      "config": {
        "useDatabusSettings": false,
        "brokerURL": "tcp://ie-databus:1883",
        "username": "",
        "password": "",
        "browseURL": "ie/m/j/simatic/v1/pnhs1/dp"
      }
    }
  ]
}
```

---

### `POST /DataService/Adapters`
**Create a new adapter.**

Creates a new adapter configuration. The adapter `name` must be unique and not empty. The `locked` parameter must be set to `false` for user-created adapters.

=== "cURL"
    ```bash
    curl -X 'POST' \
      -H 'Accept: application/json' \
      -H 'Content-Type: application/json' \
      'http://localhost:4203/DataService/Adapters' \
      -d '{
        "name": "Profinet IO Connector",
        "active": true,
        "config": {
            "brokerURL": "tcp://ie-databus:1883",
            "useDatabusSettings": false
        }
    }'
    ```

=== "Python"
    ```python
    import http.client
    import json
    
    conn = http.client.HTTPConnection("localhost:4203")
    payload = json.dumps({
        "name": "Profinet IO Connector",
        "active": True,
        "config": {
            "brokerURL": "tcp://ie-databus:1883",
            "useDatabusSettings": False
        }
    })
    headers = { 'content-type': "application/json" }
    
    conn.request("POST", "/DataService/Adapters", payload, headers)
    res = conn.getresponse()
    print(res.read().decode("utf-8"))
    ```

!!! note "Adapter Lock State"
    System adapters defaults to `"locked": true` and cannot be modified or deleted. Any adapter you create via this endpoint should be created with `"locked": false`.