<link rel="stylesheet" href="../../style.css">

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

Parameter,Type,Description
networkUri,URI,Required. The unique identifier for the Network Set. Using a Network Set allows the profile to carry multiple VLANs over a single logical connection.
ports,Array,"Defines the physical hardware paths. Specifying multiple ports (e.g., 1:1 and 1:2) enables hardware-level redundancy."

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

Status Code,Type,Description
400,Bad Request,"The JSON is malformed or missing a required field (e.g., name)."
401,Unauthorized,The auth token is missing or has expired.
403,Forbidden,"The account lacks the ""Server administrator"" permissions required to create profiles."
404,Not Found,The serverHardwareUri provided does not exist in the appliance inventory.
409,Conflict,↳ The selected server is already assigned to another profile.
500,Internal Error,An unexpected communication failure between the appliance and the hardware.

{
  "errorCode": "RESOURCE_ALREADY_ASSIGNED",
  "message": "The server hardware at /rest/server-hardware/UUID is already assigned.",
  "details": "Unassign the existing profile before attempting to create a new one.",
  "recommendedActions": [
    "Verify the hardware URI",
    "Check for existing profiles"
  ]
}

[← Back to Portfolio Home](../../)
