# System Design Roadmap

## 1. Introduction

- What is System Design?
- How to approach System Design?

## 2. Fundamentals

### Performance & Scalability

- Performance vs Scalability
- Latency vs Throughput

### Availability & Consistency

- Availability vs Consistency
- CAP Theorem
  - AP (Availability + Partition Tolerance)
  - CP (Consistency + Partition Tolerance)

### Consistency Patterns

- Weak Consistency
- Eventual Consistency
- Strong Consistency

### Availability Patterns

- Failover
  - Active-Active
  - Active-Passive
- Replication
  - Master-Slave
  - Master-Master
- Availability in Numbers
  - 99.9% (Three 9s)
  - 99.99% (Four 9s)
- Availability in Parallel vs Sequence

---

## 3. Background Jobs

- Event-Driven
- Schedule-Driven

---

## 4. Networking & Delivery

### Domain Name System (DNS)

### Content Delivery Networks (CDN)

- Push CDN
- Pull CDN

### Load Balancers

- LB vs Reverse Proxy
- Load Balancing Algorithms
- Layer 7 Load Balancing
- Layer 4 Load Balancing

---

## 5. Scaling

- Horizontal Scaling

---

## 6. Application Layer

- Microservices
- Service Discovery

---

## 7. Databases

### SQL vs NoSQL

### Database Techniques

- Replication
- Sharding
- Federation
- Denormalization
- SQL Tuning

### RDBMS

### NoSQL Types

- Key-Value Store
- Document Store
- Wide Column Store
- Graph Database

---

## 8. Caching

### Cache Strategies

- Refresh Ahead
- Write-behind
- Write-through
- Cache Aside

### Cache Locations

- Client Caching
- CDN Caching
- Web Server Caching
- Database Caching
- Application Caching

---

## 9. Asynchronous Systems

- Asynchronism
- Back Pressure
- Task Queues
- Message Queues

---

## 10. Communication

- HTTP
- TCP
- UDP
- Idempotent Operations
- RPC
- REST
- gRPC
- GraphQL

---

## 11. Performance Antipatterns

- Busy Database
- Busy Frontend
- Chatty I/O
- Extraneous Fetching
- Improper Instantiation
- Monolithic Persistence
- No Caching
- Noisy Neighbor
- Synchronous I/O Retry Storm

---

## 12. Monitoring

- Health Monitoring
- Availability Monitoring
- Performance Monitoring
- Security Monitoring
- Usage Monitoring
- Instrumentation
- Visualization & Alerts

---

## 13. Cloud Design Patterns

### Messaging

- Sequential Convoy
- Scheduler Agent Supervisor
- Queue-Based Load Leveling
- Publisher/Subscriber
- Priority Queue
- Pipes and Filters
- Competing Consumers
- Choreography
- Claim Check
- Async Request Reply

### Data Management

- Valet Key
- Static Content Hosting
- Sharding
- Materialized View
- Index Table
- Event Sourcing
- CQRS
- Cache-Aside

### Design & Implementation

- Strangler Fig
- Static Content Hosting
- Sidecar
- Pipes & Filters
- Leader Election
- Gateway Routing
- Gateway Offloading
- Gateway Aggregation
- External Config Store
- Compute Resource Consolidation
- CQRS
- Backend for Frontend (BFF)
- Anti-Corruption Layer
- Ambassador

### Reliability

#### Availability

- Deployment Stamps
- Geodes
- Health Endpoint Monitoring
- Queue-Based Load Leveling
- Throttling

#### High Availability

- Deployment Stamps
- Geodes
- Health Endpoint Monitoring
- Bulkhead
- Circuit Breaker

#### Resiliency

- Bulkhead
- Circuit Breaker
- Compensating Transaction
- Health Endpoint Monitoring
- Leader Election
- Queue-Based Load Leveling
- Retry
- Scheduler Agent Supervisor

### Security

- Federated Identity
- Gatekeeper
- Valet Key

---

## 14. Related Learning Tracks

- Backend Software Architect
- DevOps

---

## 15. Other Roadmaps

- Backend Roadmap
- DevOps Roadmap
- Software Design & Architecture

---

**Source:** Roadmap extracted from the uploaded _System Design_ roadmap. :contentReference[oaicite:0]{index=0}
