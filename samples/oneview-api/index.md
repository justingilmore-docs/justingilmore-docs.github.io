---
layout: default
title: HPE OneView API
parent: Technical Documentation
nav_order: 2
---

# HPE OneView API
## Project Context
I have modernized this legacy content into modern Markdown.
### Request Example: Multi-Interface Rack Profile
The following JSON excerpt demonstrates how to assign a **Network Set** across multiple physical ports for high-bandwidth redundancy.

```json
{
  "name": "RackProfile-Multi-NIC",
  "serverHardwareUri": "/rest/server-hardware/{serverUUID}",
  "connectionSettings": {
    "connections": [
      {
        "id": 1,
        "name": "Management-Network-Set",
        "functionType": "Ethernet",
        "networkUri": "/rest/network-sets/{networkSetUUID}",
        "ports": [
          { "portId": "Pci 1:1" },
          { "portId": "Pci 1:2" }
        ]
      }
    ]
  }
}
```

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `network_uri` | URI | **Required.** The unique identifier for the network set. Using a network set allows a profile to carry multiple VLANs over a single logical connection. |
| `ports` | Array | Defines the physical hardware path. Specifying multiple ports (e.g., `1:1` and `1:2`) enables hardware-level redundancy. |


### Example Response


**Status: 201 Created**

```json
{
  "type": "ServerProfileV12",
  "uri": "/rest/server-profiles/abc-123",
  "status": "OK",
  "taskUri": "/rest/tasks/456"
}
```

## Response Handling
The OneView API uses standard HTTP status codes. A 201 Created indicates a successful profile assignment, while 4xx codes indicate a request error that requires user intervention.

| Status Code | Type | Description |
| :--- | :--- | :--- |
| `400` | Bad Request | The server could not understand the request due to invalid syntax or missing required parameters. |
| `401` | Unauthorized | Authentication is required and has failed or has not yet been provided. Check your Bearer token. |
| `403` | Forbidden | The server understood the request but refuses to authorize it (e.g., insufficient permissions for the URI). |
| `404` | Not Found | The requested resource (Network URI or Port) could not be found on the server. |
| `409` | Conflict | The request could not be completed due to a conflict with the current state of the target resource. |
| `500` | Internal Server Error | The server encountered an unexpected condition that prevented it from fulfilling the request. |

```json
{
  "errorCode": "RESOURCE_ALREADY_ASSIGNED",
  "message": "The server hardware at /rest/server-hardware/UUID is already assigned.",
  "details": "Unassign the existing profile before attempting to create a new one.",
  "recommendedActions": [
    "Verify the hardware URI",
    "Check for existing profiles"
  ]
}
```
### Official Documentation
For complete endpoint details and real-time testing, please refer to the official API documentation:

[View Original API Reference](https://support.hpe.com/docs/display/public/dp00007443en_us/index.html#rest/server-profiles )
