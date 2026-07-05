# 📌 System Design: Resilient, Real-Time Collaborative Note-Taking Application

---

## 1. Understanding the Problem

- **What am I building in one sentence?** A highly resilient, real-time collaborative note-taking web and mobile application featuring offline-first capabilities, instant synchronization, and an advanced search pipeline.

- **Who are the users of this system?**
  - Distributed teams needing simultaneous multi-user document collaboration
  - Professionals requiring offline access to notes with automatic background syncing
  - Power users who rely on instant, highly precise full-text search across large note repositories

- **What problem does this system solve?**
  - Eliminates merge conflicts during simultaneous note editing
  - Prevents data loss during network drops via offline-first client architecture
  - Provides instant document indexing and search accuracy with zero impact on core database performance

---

## 2. Functional Requirements

### ✅ MVP & Core Features

- **Real-Time Collaborative Editing:** Multiple users can seamlessly view and edit the same note simultaneously with peer-to-peer or server-coordinated state synchronization.
- **Offline-First Capabilities:** Users can create, modify, or delete notes completely offline, with local changes securely queued and synced when connectivity is restored.
- **Rich Media Storage:** Users can upload and embed images, files, and media attachments into their notes.
- **Advanced Full-Text Search:** Instantly query notes using deep keywords, filters, and attributes.
- **Cross-Platform Access & Notifications:** Real-time push updates across browser and mobile applications.

---

## 3. Non-Functional Requirements

- **Availability & Fault Tolerance:** Multi-region resilience with fallback layers ensuring high availability (99.99% uptime).
- **Latency:** Core API responses under 100ms; collaborative cursor movements and text sync via persistent connections under 50ms.
- **Scalability:** Built horizontally to scale from 1K to millions of concurrently active users, handled by stateless application logic and specialized data pipelines.
- **Consistency Model:** Eventual consistency across clients via decentralized conflict resolution; strict audit matching to remediate background data drift.

---

## 4. Data & Storage Tier

### 📦 Storage Subsystems

- **Primary Document Store (MongoDB / DynamoDB):**
  - Houses the definitive state of notes and metadata. 
  - Optimized with composite indices on fields like `_sync_hash` and `updatedAt` for differential snapshot catching.
- **In-Memory Cache (Redis):**
  - Stores volatile user session details and reads for active/highly accessed notes to minimize database roundtrips.
- **Search Index (Elasticsearch / OpenSearch):**
  - Decoupled read-model optimized for rich queries, filtering, and text-matching scores.
- **Object Storage (AWS S3 / Google Cloud Storage):**
  - Durable immutable storage block for hosting user-uploaded images, attachments, and asset media thumbnails.

### 🔄 Event & Message Broker

- **Apache Kafka:**
  - Serves as the backbone event-streaming broker.
  - Implements **Change Data Capture (CDC)** to stream database updates asynchronously down to search indexers, reducing primary write locks.

---

## 5. High-Level Architecture

The system is strictly partitioned into specialized layers to decouple ingress traffic from core storage engines:

### 📱 1. Client Tier
- Handles frontend logic via Single Page Applications (SPA) or mobile binaries.
- Employs a **Local CRDT (Conflict-free Replicated Data Type) Replica** to facilitate immediate, conflict-free document mutations locally.
- Manages an internal **Sync Outbox Queue** that buffers client operations when offline and replays them over secure network sockets once online.
- Pulls static UI assets and media thumbnails from an Edge **CDN (CloudFront/Cloudflare)**.

### 🌐 2. Edge Tier
- **Load Balancer:** Distributes multi-protocol requests securely across nodes.
- **N* API Gateways:** Manages TLS termination, rate-limiting, and houses a **WebSocket Routing Matrix** that binds connections intelligently based on the active `Note ID`.

### ⚙️ 3. Application Tier
- **Validate Token / User Service:** Authenticates clients externally against OIDC providers (Google, Apple SSO, Auth0) and maps secure identities using an internal Vault.
- **Real-Time Collaboration Engine:** Coordinates active edits over WebSockets utilizing frameworks like Matrix or WebRTC, handling operational transformations (OT) or CRDT sync states.
- **Policy Service (OPA / Opal):** Evaluates strict Attribute/Role Access Control Lists (ACL) on every transaction.
- **Media Service:** Dispenses temporary signed URLs to allow secure, direct client uploads directly to Object Storage.
- **Search Service:** Offers a streamlined query API interacting directly with the dedicated search cluster.
- **Push Notification Service:** Coordinates event delivery to external push networks (FCM/APNS).

### 🏗️ 4. Async / Event Layer
- Monitors primary data mutation outputs using a **Kafka-driven CDC Stream**.
- Employs **Search Indexer Consumers** that manually commit operational offsets with built-in retry backoffs to securely stream text updates directly into the Elasticsearch cluster.

### 🧹 5. Reconciliation Engine
- Runs background **Reconciliation Jobs** to keep distributed storage pools structurally identical.
- **Tier 1:** Incremental checks using watermarks every ~5 minutes.
- **Tier 2:** Heavyweight **Merkle Tree Audits** run weekly to catch edge-case data drift and safely sweep orphaned tombstones.

---

## 6. API & Network Protocol Design

### 🛰️ Connection Protocols
- **HTTPS:** Reserved for synchronous, standard lifecycle requests (Auth, Media Upload Ticket Requests, Search Queries).
- **WebSockets (WSS):** Persistent, bi-directional channels dedicated to instant note updates, collaborative keystroke replication, and push status changes.

### 📋 Key API Workflows
- `POST /auth/login` ➔ Authenticates client identity and generates an active token context.
- `POST /media/signed-url` ➔ Fetches a temporary upload voucher for an attachment.
- `GET /search?q={query}` ➔ Routes directly to the search service to query the search indexes.

---

## 7. Data Flow Paths

### 📝 Real-Time Document Modification Flow
1. A user applies an edit locally; the change is immediately parsed inside the **Local CRDT Replica**.
2. The change registers into the **Sync Outbox Queue** and is dispatched across a persistent **WSS Connection**.
3. The **API Gateway** proxies the socket payload based on the matching `Note ID` to the **Real-Time Collaboration Engine**.
4. The collaboration backend writes the mutation upstream to the **Primary Document Store** and returns an ack response.
5. Concurrently, an asynchronous **CDC Event** is dispatched to **Kafka**.
6. The **Search Indexer** consumes the record from Kafka and updates the **Search Index** without hindering core app performance.

---

## 8. Resilience, Recovery, & Security

- **Drift Self-Healing:** Discrepancies introduced during unexpected race conditions or partial network breakdowns are captured by the Merkle Tree reconciliation workers and repaired automatically.
- **Dead-Letter Handling:** Failed Kafka consumer offsets leverage strict error catch-blocks with structured manual offset commits to prevent ingestion locks.
- **Granular Access Control:** Every single request entering the application layer passes through the centralized **Policy Engine** before touching storage.
- **Rate-Limiting & Edge Defense:** The API Gateway layer acts as a shield against denial-of-service threats, shielding internal micro-services from sudden surges in traffic.