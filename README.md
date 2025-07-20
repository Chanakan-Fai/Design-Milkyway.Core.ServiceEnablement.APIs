# Milkyway Core Service Enablement APIs

This repository contains the OpenAPI 3.0 specification for Milkyway Core Service Enablement APIs, used for managing SIM connectivity operations including Suspend, Reconnect, and Terminate.

## API Overview

| Endpoint | Description |
| -------- | ----------- |
| `POST /api/v2/project/{projectId}/connectivities/suspend` | Suspend SIM connectivity |
| `POST /api/v2/project/{projectId}/connectivities/reconnects` | Reconnect suspended SIMs |
| `POST /api/v2/project/{projectId}/connectivities/terminates` | Terminate SIM connectivity |

## Specification

- **Specification Format:** OpenAPI 3.0.3
- **Spec File Path:** `openapi/Milkyway.Core.ServiceEnablement.APIs.yaml`
- **Security:** OAuth2 (Client Credentials Flow), Bearer Token

## Usage

You can view, test, and interact with the APIs via:
- [SwaggerHub](https://swagger.io/tools/swaggerhub/)
- Tools like **Postman** or **Insomnia** by importing the YAML file

## Development

Feel free to fork and modify this repository as needed. For updates or issues, please raise a pull request or open an issue.

---

© 2025 AIS Milkyway Project
