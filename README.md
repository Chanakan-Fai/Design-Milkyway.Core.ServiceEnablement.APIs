# Milkyway Core Service Enablement APIs

This repository contains the **OpenAPI 3.0 specification** for the
**Milkyway Core Service Enablement APIs**, which are used to manage the
SIM connectivity lifecycle such as **Suspend**, **Reconnect**,
**Terminate**, and **Change SIM Serial**, as well as to receive
**asynchronous callbacks** from external SKY systems.

------------------------------------------------------------------------

## 📌 Overview

The APIs are divided into two main groups:

### 1️⃣ Connectivity Management APIs

Operations for managing SIM lifecycle:

-   **Suspend** -- Suspend Connectivity
-   **Reconnect** -- Reconnect Connectivity
-   **Terminate** -- Terminate Connectivity
-   **Change SIM Serial** -- Change SIM Serial

Each API supports both **JSON** and **CSV** request/response formats.

------------------------------------------------------------------------

### 2️⃣ SKY Callback APIs

These APIs are used to receive asynchronous callback results from:

-   **SKY-IOT**
-   **SKY-MPO**

Callback APIs are separated by source system to ensure:

-   Clear routing
-   Independent validation per system
-   Easier monitoring and troubleshooting
-   Source-based rate limiting

------------------------------------------------------------------------

# 🔑 Security

All APIs require authentication.

### Authorization

-   OAuth2 (Client Credentials Flow)\
    or\
-   Bearer Token

### Required Headers

  ------------------------------------------------------------------------
  Header              Required                Description
  ------------------- ----------------------- ----------------------------
  `Authorization`     ✅                      Bearer token

  `x-ais-order-ref`   ✅                      Idempotency key (must match
                                              original request reference)

  `x-ais-channel`     ✅ (Connectivity APIs)  Source channel

  `accept`            ✅                      `application/json` or
                                              `text/csv`
  ------------------------------------------------------------------------

------------------------------------------------------------------------

# 🌐 Base URL

    https://IP:PORT/Milkyway.Core.ServiceEnablement.APIs/1.0.0

------------------------------------------------------------------------

# 🟢 Connectivity APIs

Base Path:

    /api/v2/project/{projectId}/connectivities

------------------------------------------------------------------------

## 1. Suspend SIM

    POST /api/v2/project/{projectId}/connectivities/suspend

-   Suspend one or more SIMs\
-   Supports JSON array or CSV input

------------------------------------------------------------------------

## 2. Reconnect SIM

    POST /api/v2/project/{projectId}/connectivities/reconnect

-   Reconnect SIM(s) currently in Suspend state\
-   If `previousStatus = Test` → `mainPackageName` is required\
-   Change Main Package is triggered only when ATN status = Active

------------------------------------------------------------------------

## 3. Terminate SIM

    POST /api/v2/project/{projectId}/connectivities/terminates

-   Permanently terminate SIM connectivity

------------------------------------------------------------------------

## 4. Change SIM Serial

    POST /api/v2/project/{projectId}/connectivities/change-sim

-   Change SIM Serial number\
-   Supports JSON and CSV formats\
-   Validates SIM ownership and status before processing

------------------------------------------------------------------------

# 🔵 SKY Callback APIs

## SKY-IOT

Base Path:

    /api/v1/sky-iot/callback/

Payload format (all actions):

``` json
{
  "publicIdType": "iotNo",
  "publicIdValue": "9991201036",
  "privateIdType": "conductorRefId",
  "privateIdValue": "4fa7d16d-b3c6-4783-957a-bc34d78d7459",
  "orderNo": "IC-NEW-25050615115260419993",
  "statusCode": "200"
}
```

------------------------------------------------------------------------

## SKY-MPO

Base Path:

    /api/v1/sky-mpo/callback/

Register SIM example:

``` json
{
  "privateIdType": "uuid",
  "privateIdValue": "ec821f7d-f2b8-4ddf-97af-3fa19311ac51",
  "publicIdType": "mobileNo",
  "publicIdValue": "0893647975",
  "orderRefId": "CO-xxxx",
  "statusCode": "200",
  "state": "Completed",
  "stateDate": "05/09/2023 10:41:46"
}
```

------------------------------------------------------------------------

# 🔁 Callback Response

``` json
{
  "code": "200",
  "message": "Callback received successfully"
}
```

Duplicate callback handling:

    409 Conflict

------------------------------------------------------------------------

© 2025 AIS Milkyway Project -- Design and API Specification
