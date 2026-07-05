# 🎨 System Design Diagram Standards

This document defines the conventions used across all system design diagrams in this repository.

**Goals**

- Maintain consistency across diagrams.
- Improve readability.
- Make diagrams self-explanatory.
- Ensure future contributors follow the same standards.

---

# Color Coding

| Component                 | Color                   | Notes                               |
| ------------------------- | ----------------------- | ----------------------------------- |
| User / Client             | 🔵 Blue                 | Browser, Mobile App, Desktop        |
| Frontend                  | 🔵 Blue                 | Web UI, Mobile UI                   |
| Backend Services          | 🟢 Green                | APIs, Business Logic, Microservices |
| Database                  | 🟠 Orange               | SQL, NoSQL                          |
| Cache                     | 🟣 Purple               | Redis, Memcached                    |
| Message Queue / Event Bus | 🔴 Red                  | Kafka, RabbitMQ, SQS                |
| Object Storage            | 🟤 Brown                | S3, Blob Storage                    |
| CDN                       | ☁️ Light Blue           | CloudFront, Cloudflare              |
| Load Balancer             | ⚪ Gray                 | ALB, NGINX, HAProxy                 |
| External APIs             | ⚫ Gray (Dashed Border) | Third-party services                |
| Monitoring / Logging      | ⚫ Dark Gray            | Grafana, Prometheus, ELK            |

---

# Arrow Standards

## Synchronous Communication

```
Service A ─────────▶ Service B
```

- HTTP
- HTTPS
- REST
- gRPC
- RPC

Use **Solid Arrow**

---

## Asynchronous Communication

```
Producer - - - - ▶ Queue
Queue - - - - ▶ Consumer
```

Use **Dashed Arrow**

Examples:

- Kafka
- RabbitMQ
- Pub/Sub
- Event Bus

---

## Bidirectional Communication

```
Service A ◀──────▶ Service B
```

Examples:

- WebSocket
- TCP
- Peer-to-peer communication

---

## Error Flow

```
Service ──🔴──▶ Error Handler
```

Use Red arrows only when explaining failure paths.

---

## Replication / Backup

```
Primary DB =====▶ Replica DB
```

Use double/thick arrows.

---

# Shapes

| Shape             | Meaning                     |
| ----------------- | --------------------------- |
| Rectangle         | Service                     |
| Rounded Rectangle | Microservice                |
| Cylinder          | Database                    |
| Cloud             | Internet / Cloud            |
| Circle            | Event                       |
| Diamond           | Load Balancer / Decision    |
| Hexagon           | External Service (Optional) |

---

# Borders

## Solid Border

Internal components.

## Dashed Border

External systems.

Third-party APIs.

Unknown systems.

Partner services.

---

# Grouping

Always group components using containers.

Examples

```
+--------------------------------------+
| Kubernetes Cluster                   |
|                                      |
|  API Service                         |
|  Auth Service                        |
|  Payment Service                     |
+--------------------------------------+
```

Examples of groups

- Browser
- Mobile App
- Kubernetes Cluster
- Docker Network
- Availability Zone
- Region
- VPC
- Data Center

---

# Data Flow Rules

Always draw flow from

Left ➜ Right

or

Top ➜ Bottom

Avoid arrows pointing in random directions.

---

# Naming Rules

Use descriptive names.

✅ Good

```
User Service
Auth Service
Payment API
Recommendation Engine
Redis Cache
Order Database
```

❌ Bad

```
Service1
DB2
NodeA
Backend
Server
```

---

# Layout Rules

Keep users on the left.

Frontend next.

Backend next.

Data layer on the right.

External systems outside the system boundary.

Example

```
User
   │
Frontend
   │
API Gateway
   │
Microservices
   │
Database
```

---

# Diagram Legend

Every diagram should include a legend.

Example

Blue = Frontend

Green = Backend

Orange = Database

Purple = Cache

Gray = External Service

Solid Arrow = Sync Request

Dashed Arrow = Async Request

Red Arrow = Error Flow

---

# General Principles

- Keep diagrams simple.
- Avoid crossing arrows.
- Use consistent spacing.
- Align components.
- Keep labels short.
- Use one color per component type.
- Avoid unnecessary icons.
- Prefer readability over decoration.

---

# Recommended Standards

Use these architecture methodologies whenever applicable.

- C4 Model
- UML
- ArchiMate
- BPMN (for workflows)

---

# Diagram Checklist

Before committing a diagram, verify:

- [ ] Colors follow standards
- [ ] Components are grouped logically
- [ ] Arrow types are correct
- [ ] Legend is included
- [ ] Layout flows left-to-right or top-to-bottom
- [ ] Component names are descriptive
- [ ] External systems have dashed borders
- [ ] Databases use cylinder shape
- [ ] Diagram is easy to understand without explanation

---

# Version

Current Version: **1.0**

Last Updated (YYYY-MM-DD): 2026-07-05

Maintainer: Saideep Arvind Bhange

---

Following this guide ensures all architecture diagrams in this repository remain clean, professional, and consistent.
