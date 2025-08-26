
This repository contains the **OpenAPI 3.0 specification** for the **Milkyway Core Service Enablement APIs**, which are used to manage SIM connectivity lifecycle such as **Suspend**, **Reconnect**, and **Terminate**. ,and **Change Sim Serial** 

---

## 📌 Overview

The APIs provide operations for:

- **Suspend** Suspend Connectivity
- **Reconnect** Reconnect Connectivity
- **Terminate** Terminate Connectivity  
- **Change Sim Serial**  Change Sim Serial 

Each API supports both **JSON** and **CSV** request/response formats.

---


## 🔑 Security

- **Authorization:** OAuth2 (Client Credentials Flow) or Bearer Token  
- **Headers required:**
  - `x-ais-order-ref` (idempotency key, required)  
  - `x-ais-channel` (source channel, required)  
  - `authorization: Bearer <token>` (required)  
  - `accept: application/json` or `text/csv` (required)  

---

## 🚀 Endpoints

### 1. Suspend SIM
```
POST /api/v2/project/{projectId}/connectivities/suspend
```
- Suspend one or more SIMs  
- Body supports JSON array or CSV input

### 2. Reconnect SIM
```
POST /api/v2/project/{projectId}/connectivities/reconnects
```
- Reconnect SIM(s) in Suspend state  
- If `previousStatus = Test` → `mainPackageName` is required  
- Change Main Pack will be triggered only when ATN status = Active  

### 3. Terminate SIM
```
POST /api/v2/project/{projectId}/connectivities/terminates
```
- Terminate SIM connectivity permanently  

### 4. Change Sim Serial
```
POST /api/v2/project/{projectId}/connectivities/change-sim
```
- Change the Sim Serial  
- Supports both JSON and CSV formats  

---

## 📬 Responses

- **200 OK** → Operation completed or accepted  
- **202 Accepted** → Operation is in progress (async job created)  
- **400 Bad Request** → Invalid input  
- **401 Unauthorized** → Invalid or missing token  
- **500 Internal Server Error** → System error  

---

## 📖 Usage

You can:
- Import the YAML spec into **[Swagger Editor](https://editor.swagger.io)**  
- Import into **Postman** or **Insomnia**  
- Mock via **SwaggerHub** or **Prism CLI**  

---

© 2025 AIS Milkyway Project – Design and API Specification
"""

