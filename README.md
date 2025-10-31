# ABB Robot Web Services — XHTML v2.0 (OmniCore / IRC5)

 **Postman collection** to interact with **ABB OmniCore** and **IRC5** robot controllers through the **Robot Web Services (RWS)** API — **XHTML v2.0** profile.

---

## Collection Overview

This collection provides ready-to-use requests covering the main RWS services:

| Section | Description |
|----------|--------------|
| **00 – System & Controller** | System info, controller state, Auto/Manual mode management |
| **10 – Users & Privileges** | Local login, RMMP (Modify) sessions, Mastership, and role handling |
| **15 – Subscriptions** | Create, read, and delete resource subscriptions (IO, RAPID, etc.) |
| **20 – Motion System (Jog Flow)** | Jog commands, `ccount` handling, Cartesian or axis-based jogs |
| **30 – IO System** | Read and write digital or analog signals |
| **40 – RAPID Program Control** | Start / Stop / Reset PP, load/unload modules, manage tasks |
| **45 – RAPID Symbol Data** | Read and write RAPID variables |
| **50 – File Service** | Browse, upload, delete, or rename files on the controller |
| **55 – DIPC** | Data Inter-Process Communication (messaging between tasks) |
| **60 – Event Log (E-Log)** | Retrieve and clear event log entries |

---

## Requirements

- **Postman v10+**
- ABB Controller (physical or virtual)
- RWS **XHTML v2.0** profile enabled
- HTTPS connection (example: `https://127.0.0.1:55` or robot IP)
- Valid credentials (Digest or Local login)

---

## Key Variables

| Variable | Example | Description |
|-----------|----------|-------------|
| `baseUrl` | `https://127.0.0.1:55` | Controller base URL |
| `username` | `robot` | Username |
| `password` | `robot` | Password |
| `task` | `T_ROB1` | Main RAPID task |
| `module` | `MainModule` | RAPID module name |
| `signal` | `DO1` | Target IO signal |
| `domain` | `rapid` | Mastership domain |
| `ccount` | `0` | Motion system change count |
| `resources` | `/rw/iosystem/signals/Local/0/DO1;state` | Example subscription resource |

---

## How to Import

1. Open **Postman**
2. Click **Import → File**
4. Set environment variables:
- `baseUrl = https://127.0.0.1:55`
- `username` / `password` according to your setup
5. Run a simple test:  
`GET {{baseUrl}}/rw` → should return the RW index.

---

## Authentication

- **Type:** HTTP Digest *(or Local depending on configuration)*  
- Some operations (IO, RAPID, Motion) require **RMMP Modify** or **Mastership** privileges.

Example sequence:
1. `POST /users?action=set-local`
2. `POST /users/rmmp?action=request`
3. `POST /rw/mastership?action=request&domain=rapid`
4. Then execute your RAPID or IO commands

---

## 🧠 Tips & Troubleshooting

- **406 Not Acceptable:** ensure  
`Accept: application/xhtml+xml;v=2.0`
- **404 Not Found:** verify your `baseUrl` and that the controller is in **Auto mode** with motors ON.
- **Jog flow example:**  
1. Read `/rw/motionsystem?resource=change-count`  
2. Execute `POST /rw/motionsystem?action=jog` using the same `ccount`.

---

## 📄 License


© 2025 — ABB Robotics France — 

---

## 💬 Author

**Youssef Aatar**  
Engineering student at **ENSEA**, Product Expert Apprentice at **ABB Robotics France**    
GitHub: [@5RCM7](https://github.com/5RCM7)



