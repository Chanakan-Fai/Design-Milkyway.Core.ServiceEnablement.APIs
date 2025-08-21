readme_content = """# Milkyway Core Service Enablement APIs

This repository contains the **OpenAPI 3.0 specification** for the **Milkyway Core Service Enablement APIs**, which are used to manage SIM connectivity lifecycle such as **Suspend**, **Reconnect**, and **Terminate**.

---

## 📌 Overview

The APIs provide operations for:

- **Suspend** SIM connectivity  
- **Reconnect** suspended SIMs (with optional main package change)  
- **Terminate** SIM connectivity  
- **Change Main Package**  

Each API supports both **JSON** and **CSV** request/response formats.

---

## 📂 Repository Structure

```
/
├── README.md
├── v1.0.0/
│   └── Milkyway.Core.ServiceEnablement.APIs.yaml
```

- **README.md** → Documentation of the project  
- **v1.0.0/** → OpenAPI specs for version 1.0.0  

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

### 4. Change Main Package
```
POST /api/v2/project/{projectId}/connectivities/change-main-pack
```
- Change the main package of SIM(s)  
- Supports both JSON and CSV formats  

---

## 📝 Example Request (JSON)

```json
[
  {
    "mobileNo": "0829921384",
    "simSerial": "2430004100504",
    "taxId": "678123421111401",
    "mainPackageName": "SmartwayFleetManagementAPN60BFixIPCorp"
  }
]
```

## 📊 Example Request (CSV)

```
mobileNo,simSerial,taxId,mainPackageName
0829921384,2430004100504,678123421111401,SmartwayFleetManagementAPN60BFixIPCorp
```

---

## 📬 Responses

- **200 OK** → Operation completed or accepted  
- **202 Accepted** → Operation is in progress (async job created)  
- **400 Bad Request** → Invalid input  
- **401 Unauthorized** → Invalid or missing token  
- **500 Internal Server Error** → System error  

---

## 🔔 Notification

- After operations complete, notification/email will be triggered according to project policies.

---

## 📖 Usage

You can:
- Import the YAML spec into **[Swagger Editor](https://editor.swagger.io)**  
- Import into **Postman** or **Insomnia**  
- Mock via **SwaggerHub** or **Prism CLI**  

---

© 2025 AIS Milkyway Project – Design and API Specification
"""

# สร้างไฟล์ README.md
file_path = "/mnt/data/README.md"
with open(file_path, "w", encoding="utf-8") as f:
    f.write(readme_content)

file_path
