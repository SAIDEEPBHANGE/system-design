# 📌 System Design Questions Checklist (Universal) - TinyURL Case Study

Use this checklist before starting ANY system design project.

---

## 1. Understanding the Problem

- **What am I building in one sentence?**
  - We are building a scalable URL Shortening service that takes long URLs and converts them into short, unique aliases, and redirects users to the original URL when the short link is accessed.
- **Who are the users of this system?**
  - General internet users, social media marketers, and third-party applications consuming our shortening APIs.
- **What problem does this system solve?**
  - Long, complex URLs are difficult to share, consume character limits on platforms like Twitter, and look unappealing. Short URLs save space, look clean, and are easier to track.

---

## 2. Functional Requirements

- **What features must the system support?**
  - Generating a unique short alias for a given long URL (e.g., `https://tiny.cc/ab12cd`).
  - Redirecting users to the original long URL quickly when they click the short link.
- **What can a user do in this system?**
  - Paste a long URL to get a short URL, and optionally provide a custom alias for their link.
- **What are the MVP (must-have) features?**
  - URL Shortening and high-speed HTTP Redirection.
- **What are future / optional features?**
  - Link expiration (automatic deletion after a set time) and detailed analytics (tracking clicks, location, device type).

---

## 3. Non-Functional Requirements

- **How fast should the system be?**
  - The redirection must be extremely fast. Read latency should be under 100–150 milliseconds (ms).
- **How many users should it support? / What is the expected scale?**
  - 500 Million new URLs created per month and 5 Billion clicks/redirections per month (highly Read-Heavy system with a 10:1 Read-to-Write ratio).
  - Roughly 200 Write Requests/sec and 2,000 Read Requests/sec (Total QPS ≈ 2,200).
- **Do we need real-time features?**
  - No real-time features like chat are required, but updates should propagate quickly.
- **Should we optimize for availability or consistency?**
  - **Availability:** The system must be highly available (99.99% uptime). We favor availability over strict consistency (Eventual Consistency is acceptable if a newly updated link takes a second to sync across all servers).

---

## 4. Data & Storage

- **What data needs to be stored?**
  - `ShortURL` (Short code/hash), `OriginalURL` (Long URL), `UserID` (Owner ID), and timestamps like `CreatedAt` and `ExpiredAt`.
- **Which database is suitable (SQL / NoSQL)?**
  - **NoSQL (e.g., MongoDB or Cassandra):** Since we need to store billions of rows with zero complex relations/joins between them. NoSQL handles key-value reads and writes at massive scale much faster than relational databases.
- **What is the data schema?**
  - A simple `Mapping Table`: ShortURL (String - Primary Key) | OriginalURL (String) | UserID (Int) | CreatedAt (Timestamp)
- **How will we query the data efficiently? / Do we need indexing?**
  - The `ShortURL` will act as the Primary Key and will be heavily indexed so that fetching the original URL takes $O(1)$ or near $O(1)$ time complexity.

---

## 5. API Design

- **What APIs are needed? / What are the main endpoints?**
  - 1. `POST /api/v1/shorten` (To create a short link)
  - 2. `GET /{short_url_code}` (To redirect the user)
- **What are request/response formats?**
  - `POST` Request Body (JSON): `{"original_url": "...", "custom_alias": "..."}`
  - `POST` Response Body (JSON): `{"short_url": "...", "created_at": "..."}`
- **How will authentication work?**
  - Publicly accessible for guest users. Registered users will use **JWT Tokens** or **API Keys** to track usage limits and access custom dashboards.
- **REST or event-based design?**
  - Standard **REST API** design is ideal and sufficient for this project.

---

## 6. High-Level Architecture

- **What are the main components?**
  - Clients (Web/Mobile), Load Balancer, Application Servers (API Layer), Key Generation Service (KGS), Redis Cache, and the NoSQL Database Cluster.
- **Do we need frontend + backend separation?**
  - Yes, decoupled frontend (React/HTML) and scalable backend services (Node.js/Go/Java).
- **Do we need a load balancer?**
  - Yes, to distribute the heavy incoming QPS evenly across multiple application servers.
- **Do we need caching?**
  - Yes, **Redis Cache** is critical to store frequently accessed URLs in RAM to protect the database from melting under high traffic.
- **Do we need message queues?**
  - Not initially for basic routing, but **Kafka** or **RabbitMQ** will be needed later to process heavy analytics logs asynchronously without blocking the main redirection flow.

---

## 7. Data Flow

- **What happens step-by-step for a user action?**
  - **Read Flow (Clicking a link):** User clicks short link -> Request hits Load Balancer -> Routed to an App Server -> Server checks **Redis Cache** -> If **Cache Hit**, returns original URL immediately -> If **Cache Miss**, queries NoSQL Database, updates the Cache, and returns the original URL.
- **Where is data written and read?**
  - New links are strictly written to the main NoSQL Database. Reads hit the Cache layer first, falling back to the Database on a miss.
- **What happens on success and failure?**
  - On Success: HTTP Status `302 Found` performs the redirection. On Failure (Link not found): HTTP Status `404 Not Found` page is served.

---

## 8. Scalability

- **What happens if traffic increases 10x?**
  - Storage will hit limits faster (150 TB instead of 15 TB over 5 years), and the read QPS will surge to 20,000 requests/sec.
- **What is the first bottleneck?**
  - Database Read I/O will become the bottleneck as thousands of concurrent read requests try to query disk storage simultaneously.
- **Do we need multiple servers? / Do we need horizontal scaling?**
  - Yes, we will apply **Horizontal Scaling** to spin up more App Servers and apply **Database Sharding/Partitioning** based on the hash of the short URL code.
- **What should be cached?**
  - The top 20% most popular links (**80-20 Rule**), which account for 80% of total daily traffic.

---

## 9. Reliability & Failure Handling

- **What if database goes down?**
  - We use **Master-Slave Replication**. The Master node handles writes, while multiple Slave nodes handle reads. If the Master goes down, a Slave node automatically gets promoted to Master.
- **What if server crashes?**
  - The Load Balancer uses heartbeat checks to detect dead servers and immediately shifts traffic to active healthy nodes.
- **What if network fails? / Do we need retries?**
  - Implement internal retries with **Exponential Backoff** at the network/API layer.
- **Do we need backups?**
  - Daily automated snapshots/backups of the NoSQL database stored securely on cloud object storage (like AWS S3).

---

## 10. Security

- **How do we authenticate users? / How do we authorize actions?**
  - Standard User Authentication allows users to manage, edit, or delete only their owned links.
- **How do we protect APIs? / Do we need rate limiting?**
  - A **Rate Limiter** is placed at the entrance to prevent bad actors or bots from abusing the system (e.g., max 100 requests per minute per IP address to prevent DDoS).
- **Is data encrypted?**
  - Yes, data in transit is encrypted using HTTPS (SSL/TLS).

---

## 11. Optimization

- **What can be cached? / Can we reduce database load?**
  - Caching hot URLs completely isolates the database from 80% of the read load.
- **What can be precomputed?**
  - **Key Generation Service (KGS):** Instead of calculating a short code during the request runtime, a standalone service pre-generates millions of unique 7-character strings beforehand and saves them. When a user creates a link, KGS just gives a ready-made code instantly, dropping execution times.

---

## 12. Trade-offs

- **SQL vs NoSQL — why?**
  - NoSQL scales out horizontally with ease and offers rapid key-value performance. We don't require heavy relational features or multi-table JOINs found in SQL.
- **Consistency vs availability?**
  - High Availability is favored over strict consistency. It's okay if a newly updated link takes 1-2 seconds to reflect worldwide, as long as the site doesn't go completely offline.
- **Performance vs cost?**
  - Using a large Redis Cache increases RAM infrastructure costs but guarantees rapid sub-100ms speeds for the end-user.

---

## 13. Future Improvements

- **What features can be added later?**
  - Advanced user analytics dashboards showing detailed traffic source graphs.
- **How will system evolve?**
  - As traffic hits Petabyte-scale, we will move towards a **Geo-Distributed Architecture**, running servers globally close to users (e.g., India servers for Asia traffic, US servers for America traffic) using a CDN (Content Delivery Network).
