# SiteEdge API Reference Guide

**Version:** 2.4  
**Base URL:** `https://api.siteedge.io/v2`  
**Authentication:** Bearer Token

---

## Overview

The SiteEdge REST API provides programmatic access to industrial site monitoring 
data, device configuration, and alert management. Use this API to integrate 
SiteEdge data into your enterprise dashboards, CMMS platforms, or custom workflows.

---

## Authentication

All API requests require a Bearer token in the `Authorization` header.
```http
Authorization: Bearer <your_token>
```

To generate a token, navigate to **Settings → API Access → Generate Token** 
in the SiteEdge portal.

---

## Endpoints

### Devices

#### GET /devices

Returns a list of all registered devices in your organization.

**Request**
```http
GET /devices
Authorization: Bearer <your_token>
```

**Response**
```json
{
  "devices": [
    {
      "id": "dev-001",
      "name": "Compressor Unit A",
      "status": "online",
      "location": "Plant Floor 2",
      "last_seen": "2026-03-17T08:42:00Z"
    }
  ],
  "total": 1
}
```

**Response fields**

| Field | Type | Description |
|---|---|---|
| `id` | string | Unique device identifier |
| `name` | string | Human-readable device name |
| `status` | string | `online`, `offline`, or `warning` |
| `location` | string | Physical location label |
| `last_seen` | string | ISO 8601 timestamp of last ping |

---

#### GET /devices/{id}

Returns details for a single device.

**Path parameters**

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | string | Yes | Device ID |

**Request**
```http
GET /devices/dev-001
Authorization: Bearer <your_token>
```

**Response**
```json
{
  "id": "dev-001",
  "name": "Compressor Unit A",
  "status": "online",
  "location": "Plant Floor 2",
  "firmware": "v3.1.2",
  "alerts": []
}
```

---

### Alerts

#### GET /alerts

Returns all active alerts across your organization.

**Query parameters**

| Parameter | Type | Required | Description |
|---|---|---|---|
| `severity` | string | No | Filter by `low`, `medium`, or `high` |
| `device_id` | string | No | Filter by device |

**Request**
```http
GET /alerts?severity=high
Authorization: Bearer <your_token>
```

**Response**
```json
{
  "alerts": [
    {
      "id": "alert-204",
      "device_id": "dev-001",
      "severity": "high",
      "message": "Temperature threshold exceeded",
      "triggered_at": "2026-03-17T07:15:00Z"
    }
  ]
}
```

---

## Error codes

| Code | Meaning |
|---|---|
| `400` | Bad request — check your parameters |
| `401` | Unauthorized — invalid or missing token |
| `404` | Resource not found |
| `429` | Rate limit exceeded |
| `500` | Internal server error |

---

## Rate limits

The API allows **1,000 requests per hour** per token. 
Exceeding this limit returns a `429` response. 
The `Retry-After` header indicates when you can retry.