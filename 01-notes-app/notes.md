# 🧠 Project Notes - Notes App

---

# 📌 What I Learned from the Notes App System Design Project

- Gained a solid understanding of **System Design fundamentals** and how scalable applications are architected.

- Learned about the **C4 Architecture Model**, which provides a structured way to visualize software architecture at multiple levels of abstraction.

- Understood how **Load Balancers** distribute incoming traffic across multiple servers to improve scalability, availability, and fault tolerance.

- Explored the purpose of **API Gateways** and how they manage, authenticate, and route client requests to backend services.

- Studied the different architectural tiers involved in the system, including:
  - **Client Application Tier**
  - **Application/Service Tier**
  - **Data Tier**
  - **Infrastructure Tier**

- Learned about **Event-Driven Architecture** and the importance of **Asynchronous Processing** for building efficient and responsive applications.

- Understood how a **Content Delivery Network (CDN)** improves application performance by reducing latency and serving static content from geographically distributed servers.

- Developed an understanding of software architecture design methodologies, including **Top-Down** and **Left-to-Right** architectural planning.

- Designed **four different versions** of the Notes App architecture, starting from a high-level overview and progressively refining it into a detailed system design covering all critical components.

- Learned how **WebSockets** enable real-time, bidirectional communication between clients and servers.

- Improved my understanding of **HTTPS (Hypertext Transfer Protocol Secure)** and the importance of secure communication in modern web applications.

- Explored **CRDTs (Conflict-Free Replicated Data Types)** and understood how they maintain data consistency across distributed systems without conflicts.

- Gained insights into the differences between **Offline-First** and **Online-First** application architectures.

- Learned how offline applications synchronize local changes with the server using the **Sync-Outbox Pattern**, ensuring reliable data synchronization after connectivity is restored.

- Enhanced my understanding of designing **scalable**, **reliable**, **secure**, and **maintainable** distributed systems by integrating concepts such as:
  - C4 Architecture
  - Load Balancing
  - API Gateways
  - Multi-Tier Architecture
  - Event-Driven Systems
  - Asynchronous Processing
  - CDN
  - WebSockets
  - HTTPS
  - CRDTs
  - Offline Synchronization

---

## 🤔 My Initial Thinking

Before starting the system design, I had a very basic understanding of how a software system was structured. My assumptions were based on the projects I had previously worked on, but I had never designed an entire system from scratch.

### What did I think the system would look like?

Initially, I imagined the architecture as a very simple three-component system:

- **Client** → where users interact with the application.
- **Server** → responsible for handling requests and business logic.
- **Database** → used for storing and retrieving data.

I simply connected these components with arrows to represent the flow of requests and responses, without considering scalability, reliability, or performance.

### What components did I assume?

Before working on this project, I assumed that every application consisted of only three major layers:

- **Client Layer**
- **Backend/Server Layer**
- **Database Layer**

Since I had never designed a complete system from scratch, I also relied on **Artificial Intelligence** to validate my understanding and help correct mistakes during the learning process.

However, through this project, I realized that modern distributed systems are much more sophisticated and include several additional architectural layers, such as:

- **Client Layer**
- **Edge Layer** (CDN, Load Balancer, API Gateway)
- **Application/Service Layer**
- **Asynchronous Event Layer**
- **Data Layer**

This project significantly changed my perspective on system architecture and helped me understand how each layer contributes to building scalable, reliable, and maintainable applications.

---

## 🏗️ What I Actually Built (V01)

Version 1 was the most basic representation of the Notes App architecture. The primary goal was to understand the fundamental flow of data between the client and the server before introducing advanced system design concepts.

### Architecture Overview

The system consisted of the following components:

- **User**
- **Notes Frontend**
- **HTTP Requests**
- **REST API (Backend)**
- **Database**

### Request Flow

1. The **User** interacts with the **Notes Frontend**.
2. The frontend sends **HTTP requests** to the backend using **REST APIs**.
3. The backend processes the incoming requests.
4. The backend executes the required database queries.
5. The **Database** stores or retrieves the requested notes.
6. The backend returns the response to the frontend, which is then displayed to the user.

### Key Characteristics

- A simple **Client → Backend → Database** architecture.
- Communication was entirely based on **HTTP** and **REST APIs**.
- No authentication, caching, load balancing, CDN, or scalability mechanisms were included.
- Built as a starting point to understand the basic request-response lifecycle before moving to more advanced system designs.

---

## 🔄 Evolution of Design

### 🏗️ V01 – Basic Architecture

Version 1 was my first attempt at designing the Notes App system. At this stage, I had very little knowledge of system design and focused only on understanding the basic request-response flow.

#### Architecture

- **User**
- **Notes Frontend**
- **HTTP Requests**
- **REST API (Backend)**
- **Database**

#### Request Flow

```text
User
   │
   ▼
Notes Frontend
   │ (HTTP Request)
   ▼
Backend REST APIs
   │ (Database Queries)
   ▼
Database
```

#### What I Learned

- Built a simple **Client → Backend → Database** architecture.
- Used **HTTP** for communication between the client and backend.
- Used **REST APIs** to expose backend functionality.
- The backend directly executed database queries.
- Designed only for a **single user** scenario.
- Did not consider:
  - Scalability
  - Authentication
  - Authorization
  - Real-time collaboration
  - Performance optimization
  - Multiple users editing the same note
  - System reliability

This version served as the foundation for everything I learned later.

---

### 🏗️ V02 – Introducing Layered Architecture

While designing Version 2, I started learning standard system design practices and architectural principles.

One of the biggest improvements was understanding that system architecture should follow a structured layout, such as:

- **Top-to-Bottom**
- **Left-to-Right**

I also learned about the **C4 Architecture Model**, which helped me organize the system into logical layers.

#### Layers Added

- **Client Tier**
- **Edge Tier**
- **Application Tier**
- **Data Tier**

#### Improvements

##### Client Tier

- Added **State Management** for better UI performance.
- Added **Local Storage** to improve the client experience.

##### Edge Tier

- Added a **Load Balancer**.
- Introduced **Authentication Routing**.
- Added **WebSockets** for real-time communication.

##### Application Tier

Created dedicated backend services, including:

- User Service
- Notes Service
- Authentication Service
- Real-Time Collaboration Service
- WebSocket Service

##### Data Tier

Introduced multiple storage components instead of relying on a single database:

- **In-Memory Cache** for faster data access.
- **Distributed Document Store (NoSQL)** for storing notes.
- **Permission Graph** for managing user permissions and note access.

#### Key Takeaways

Compared to V01, this version focused more on scalability, modularity, and separation of responsibilities.

---

### 🏗️ V03 – Advanced Distributed System Design

Version 3 was the biggest milestone in my learning journey. This was the point where I started designing the system in a more professional and structured way.

#### Major Improvements

##### Asynchronous Event Layer

One of the biggest additions was introducing an **Asynchronous Event Layer**.

This layer was responsible for:

- Event processing
- Notification mechanisms
- Background processing
- Decoupling services

##### Security Enhancements

Added several security-related concepts, including:

- **TLS (Transport Layer Security)** for secure communication.
- Authentication validation.
- Authorization mechanisms.
- **Access Control Lists (ACLs)** for controlling note permissions.

##### Monitoring

Added a dedicated **Monitoring System** to observe the health of the application and backend services.

##### Diagram Standardization

For the first time, I also standardized my architecture diagrams by introducing:

- Color-coded components
- Legends
- Consistent arrow styles
- Clear representation of data flow and communication

This made the diagrams much easier to understand and more aligned with professional architecture documentation.

#### Why This Version Was Important

Version 3 transformed the design from a simple architecture diagram into a much more complete distributed system that considered security, observability, maintainability, and real-time communication.

---

### 🏗️ V04 – Error Handling & Logging

Version 4 focused on improving the reliability and maintainability of the system.

#### New Features

- Added a centralized **Error Handling Mechanism**.
- Connected the error handling system with the **Monitoring Service**.
- Integrated a **Logging System** to capture application and infrastructure errors.

#### Benefits

- Errors can be detected and recorded automatically.
- Logs help identify failures and simplify debugging.
- Monitoring and logging together improve system observability and operational reliability.

Although Version 4 introduced fewer architectural components than Version 3, it significantly improved the production readiness of the overall system.

---

## ⚙️ Key Concepts I Learned

Throughout this project, I gained both theoretical knowledge and practical experience in modern system design. The following are the key concepts I learned:

- **Client-Server Communication**
- **HTTP Request–Response Lifecycle**
- **REST APIs**
- **Database CRUD Operations**
- **Request Flow**
- **Basic System Architecture**
- **C4 Architecture Model**
- **Layered Architecture (Client, Edge, Application, Event, and Data Tiers)**
- **Load Balancing**
- **API Gateway**
- **Authentication & Authorization**
- **Permission Management**
- **Role-Based Access Control (RBAC)**
- **Access Control Lists (ACLs)**
- **WebSockets for Real-Time Communication**
- **Real-Time Collaboration**
- **Event-Driven Architecture**
- **Asynchronous Processing**
- **Notification Mechanisms**
- **Content Delivery Network (CDN)**
- **Caching Strategies**
- **In-Memory Cache**
- **Distributed NoSQL Document Stores**
- **HTTPS & TLS Security**
- **Scalable System Design Principles**
- **Top-to-Bottom and Left-to-Right Architecture Design Approaches**
- **Monitoring & Observability**
- **Logging and Error Handling**
- **Distributed System Fundamentals**
- **Conflict-Free Replicated Data Types (CRDTs)**
- **Offline-First vs Online-First Application Design**
- **Sync-Outbox Pattern for Offline Synchronization**
- **State Management**
- **Local Storage**
- **Designing Multi-Service (Microservice-Oriented) Architectures**
- **Creating Professional Architecture Diagrams with Standardized Layers, Legends, and Data Flow**

---

## ⚠️ Mistakes I Made

Throughout this project, I made several mistakes that became valuable learning experiences. These helped me improve both my system design thinking and my overall architectural approach.

- I started drawing the architecture before fully understanding the functional and non-functional requirements.

- Initially, I assumed that a system only consisted of a **Client**, **Backend**, and **Database**, without considering other architectural layers.

- I did not think about **scalability** while designing the first version.

- I ignored **authentication** and **authorization** in the initial design.

- I did not consider **multiple users collaborating** on the same note at the same time.

- I overlooked **real-time communication** and did not include WebSockets in the early versions.

- I forgot to define clear **API endpoints** and service responsibilities before designing the architecture.

- I did not think about **failure scenarios**, such as server failures, network issues, or database outages.

- Initially, I ignored **caching**, which could improve application performance.

- I was not aware of the importance of an **Edge Layer**, including components such as Load Balancers, API Gateways, and CDNs.

- I designed everything as a single backend instead of separating responsibilities into multiple services.

- I underestimated the importance of **asynchronous processing** and **event-driven architecture**.

- I did not consider **offline-first** application behavior or data synchronization strategies in the beginning.

- I overlooked **monitoring**, **logging**, and **error handling**, which are essential for production systems.

- My first architecture diagrams lacked proper structure, legends, standardized colors, and clear data flow, making them difficult to understand.

- Instead of thinking from the user's requirements first, I initially focused only on connecting components together.

### 💡 Biggest Lesson

The biggest lesson I learned is that **system design is not just about connecting boxes with arrows**. It begins with understanding the requirements, identifying constraints, considering scalability and reliability, and then choosing the right architectural components to solve those problems effectively.

---

## 🧩 Questions That Confused Me (Along with What I Learned)

### 1. Why do we need a Load Balancer?

**Answer:**
A **Load Balancer** distributes incoming client requests across multiple backend servers instead of sending all traffic to a single server.

**Benefits:**

- Prevents one server from becoming overloaded.
- Improves availability and fault tolerance.
- Enables horizontal scaling by adding more servers.
- Removes unhealthy servers from traffic automatically.

---

### 2. When should I use Cache?

**Answer:**
Caching should be used for data that is **read frequently but changes infrequently**.

**Examples:**

- User profiles
- Frequently accessed notes
- Application settings
- Search results

**Benefits:**

- Reduces database load.
- Improves response time.
- Lowers server latency.
- Enhances user experience.

---

### 3. SQL vs NoSQL — When should I use what?

| SQL               | NoSQL                               |
| ----------------- | ----------------------------------- |
| Structured data   | Flexible schema                     |
| ACID transactions | High scalability                    |
| Complex joins     | Fast document retrieval             |
| Banking systems   | Chat apps, Notes apps, Social media |

**Rule of Thumb**

- Use **SQL** when data consistency and relationships are critical.
- Use **NoSQL** when scalability, flexibility, and high throughput are more important.

---

### 4. How does a Push Gateway work?

**Answer:**
A **Push Gateway** allows short-lived jobs (such as cron jobs or batch processes) to push their metrics to a central gateway. A monitoring system (like Prometheus) then scrapes metrics from the Push Gateway instead of directly from the temporary jobs.

---

### 5. How does a Message Bus work?

**Answer:**
A **Message Bus** enables services to communicate asynchronously.

**Flow**

```
Service A
     │
Publish Event
     │
     ▼
Message Bus
     │
 ┌───┼────┐
 ▼   ▼    ▼
Service B
Service C
Service D
```

**Benefits**

- Loose coupling
- Better scalability
- Reliable event delivery
- Independent services

---

### 6. What is the Single Writer Pattern and its Locking Mechanism?

**Answer:**
The **Single Writer Pattern** ensures that only one process is allowed to modify a particular piece of data at a time.

Instead of multiple services updating the same record simultaneously:

```
Multiple Writers ❌

Writer 1 → Note
Writer 2 → Note
Writer 3 → Note
```

It becomes:

```
Single Writer ✅

Writer
   │
   ▼
Database
```

**Benefits**

- Prevents race conditions.
- Avoids conflicting updates.
- Maintains data consistency.

---

### 7. What is Apache Kafka, and how does it help in Search Indexing?

**Answer:**
**Apache Kafka** is a distributed event streaming platform.

Whenever a note is created or updated:

```
User edits note
      │
      ▼
Database
      │
      ▼
Kafka Topic
      │
      ▼
Search Indexer
      │
      ▼
Search Engine
```

The Search Indexer consumes events from Kafka and updates the search index, ensuring searchable data stays synchronized without slowing down the main application.

---

### 8. What is Manual Offset Commit?

**Answer:**
Kafka keeps track of which messages a consumer has processed using **offsets**.

With **Manual Offset Commit**, the consumer acknowledges a message **only after successful processing**.

**Benefit**
If processing fails, Kafka can re-deliver the message, preventing data loss.

---

### 9. What is a Reconciliation Job?

**Answer:**
A **Reconciliation Job** periodically compares data between two systems to detect and repair inconsistencies.

**Example**

```
Database
     │
Compare
     │
Search Index
```

If differences are found, missing or outdated records are synchronized automatically.

---

### 10. What are Incremental Sync, Bucket Hash Audit, and Tombstones?

#### Incremental (Watermark) Synchronization

Only records updated after the last successful synchronization are processed.

**Benefit**

- Faster synchronization.
- Less bandwidth usage.

---

#### Bucket Hash Audit (Weekly)

Instead of comparing every record, data is divided into buckets.

Each bucket generates a hash.

If hashes differ:

- Only that bucket is rechecked.

This makes large-scale consistency verification much faster.

---

#### Tombstones (Delete Diff)

When a record is deleted, a special delete marker (**tombstone**) is stored or published.

Other services receive the tombstone and delete the corresponding data, keeping all systems synchronized.

---

### 11. What is a Search Index and `_syncHash`?

**Search Index**

A Search Index is an optimized data structure that enables fast search operations instead of querying the main database for every search request.

Examples include **Elasticsearch**, **OpenSearch**, and **Apache Solr**.

**`_syncHash`**

A `_syncHash` is a checksum or hash representing a document's content.

During synchronization:

- If hashes match → document is already synchronized.
- If hashes differ → document needs to be updated.

This avoids unnecessary updates and improves synchronization efficiency.

---

### 12. How do WebSockets work?

**Answer:**
Unlike HTTP, which creates a new connection for each request, **WebSockets** maintain a persistent connection between the client and server.

This enables real-time communication such as:

- Collaborative note editing
- Live cursors
- Instant notifications
- Chat applications

---

### 13. How do CRDTs resolve conflicts?

**Answer:**
**Conflict-Free Replicated Data Types (CRDTs)** allow multiple users to edit the same document simultaneously without central coordination.

Each device maintains its own copy of the data.

When synchronization occurs, CRDT algorithms automatically merge changes into a consistent final state without conflicts.

---

### 14. How do Offline-First applications synchronize data?

**Answer:**
Offline-first applications save user actions locally.

When internet connectivity is restored:

1. Pending operations are stored in a Sync-Outbox.
2. Changes are uploaded to the server.
3. Conflicts are resolved (using mechanisms such as CRDTs).
4. The local copy is updated with the latest synchronized data.

---

### 15. Why is Asynchronous Processing important?

**Answer:**
Instead of waiting for every operation to complete immediately, asynchronous processing allows long-running tasks to execute in the background.

Examples include:

- Sending notifications
- Email delivery
- Search indexing
- Analytics processing

**Benefits**

- Faster API responses.
- Better scalability.
- Improved user experience.

---

### 16. Why are Monitoring, Logging, and Alerting important?

**Monitoring**

- Tracks system health and performance.

**Logging**

- Records application events and errors.

**Alerting**

- Notifies engineers when predefined thresholds or failures occur.

Together, they make production systems easier to operate, debug, and maintain.

---

## 💡 Improvements I Discovered Later

As I continued improving my Notes App system design, I realized several important principles that I should have followed from the beginning. These lessons significantly improved the quality of my architecture.

- **Always start by understanding the requirements** before drawing any architecture diagram.
  - Identify both **functional** and **non-functional** requirements.
  - Understand the target users, expected traffic, performance goals, and system constraints.

- **Think about scalability early** instead of treating it as an afterthought.
  - Estimate the number of users.
  - Consider read/write traffic.
  - Plan for horizontal scaling if required.

- **Version the architecture** instead of trying to design the perfect system in one attempt.
  - V01 → Basic Architecture
  - V02 → Layered Architecture
  - V03 → Distributed & Event-Driven Architecture
  - V04 → Production-Ready Improvements

- **Design from high-level to low-level** using a structured approach such as the **C4 Architecture Model**.

- **Separate responsibilities into layers** instead of putting everything inside a single backend service.
  - Client Tier
  - Edge Tier
  - Application Tier
  - Event Tier
  - Data Tier

- **Think about security from the beginning**, including:
  - Authentication
  - Authorization
  - HTTPS/TLS
  - Access Control

- **Plan for concurrent users** instead of assuming only one user will use the application.
  - Real-time collaboration
  - Conflict resolution
  - Permission management

- **Consider offline support** early if the application should work without an internet connection.
  - Local Storage
  - Sync-Outbox Pattern
  - Data synchronization

- **Use asynchronous processing** for long-running tasks rather than making users wait.
  - Notifications
  - Search indexing
  - Background jobs

- **Introduce caching only where it provides value** instead of querying the database for every request.

- **Design for failure**, not just for success.
  - Server failures
  - Network interruptions
  - Database outages
  - Retry mechanisms
  - Graceful error handling

- **Include observability from the start.**
  - Monitoring
  - Logging
  - Alerting
  - Error tracking

- **Create standardized architecture diagrams** with:
  - Consistent colors
  - Legends
  - Clear labels
  - Well-defined data flow
  - Proper component grouping

- **Document architectural decisions** so that future improvements and design choices are easy to understand.

### 🚀 Biggest Improvement

The biggest improvement in my thinking was realizing that **system design is an iterative process**. Rather than trying to build the perfect architecture on the first attempt, it is better to start with a simple design, validate it, identify limitations, and continuously refine it through multiple versions.

---

## 🚀 What I Would Do Differently Next Time

If I were to redesign this project from scratch, I would approach it much more systematically based on the lessons I learned throughout the process.

- **Start with a checklist** before drawing any architecture.
  - Gather all functional requirements.
  - Identify non-functional requirements (scalability, reliability, security, performance).
  - Define assumptions and constraints.
  - List possible edge cases.

- **Design the APIs before designing the architecture.**
  - Define REST endpoints.
  - Identify request and response models.
  - Plan authentication and authorization.
  - Clearly define service responsibilities.

- **Think about failure scenarios early.**
  - What happens if a server crashes?
  - What if the database becomes unavailable?
  - How should the system recover from failures?
  - How should retries, logging, and monitoring work?

- **Estimate scale before choosing technologies.**
  - Expected number of users.
  - Read/write traffic.
  - Storage requirements.
  - Network bandwidth.

- **Design for real-world usage instead of ideal scenarios.**
  - Multiple users editing the same note.
  - Offline synchronization.
  - Real-time collaboration.
  - Concurrent requests.

- **Separate the system into well-defined architectural layers** from the beginning instead of refactoring later.

- **Include observability from day one.**
  - Monitoring
  - Logging
  - Error handling
  - Alerting

- **Iteratively improve the architecture** rather than trying to build the final design in a single attempt.

---

## 📌 Final Understanding (After Completion)

Completing this project completely changed the way I think about software architecture and distributed systems. What started as a simple client-server diagram evolved into a layered, scalable, and production-oriented system design.

### What I Learned

- **System design is about making trade-offs**, not finding one perfect solution.

- **Every architectural component exists to solve a specific problem.**
  - Load Balancer → Scalability
  - API Gateway → Request routing & security
  - Cache → Performance
  - WebSockets → Real-time communication
  - Event Bus → Asynchronous processing
  - Monitoring → Observability
  - Logging → Debugging
  - CRDTs → Conflict resolution
  - CDN → Faster content delivery

- **A good architecture evolves over time.**
  - Start simple.
  - Identify limitations.
  - Improve incrementally.
  - Version the design instead of replacing it.

- **Requirements should always come before technology choices.**

- **Scalability, reliability, security, and maintainability should be considered from the beginning**, not added later.

- **System design is much more than drawing boxes and arrows.** It involves understanding user requirements, designing communication between components, planning for failures, handling concurrent users, optimizing performance, and ensuring the system can evolve as requirements grow.

### 🎯 Final Takeaway

This project was not just about designing a **Notes App**—it was about learning **how to think like a System Designer**. Through four iterations (V01 → V04), I developed a much stronger understanding of distributed systems, layered architecture, real-time communication, offline synchronization, event-driven design, and production-ready software architecture. It also taught me that continuous iteration and learning are essential parts of building scalable and reliable systems.
