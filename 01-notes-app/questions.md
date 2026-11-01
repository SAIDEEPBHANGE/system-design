# 📌 System Design Questions Checklist (Universal)

Use this checklist before starting ANY system design project.

---

## 1. Understanding the Problem

- What am I building in one sentence?
- Who are the users of this system?
- What problem does this system solve?

---

## 2. Functional Requirements

- What features must the system support?
- What can a user do in this system?
- What are the MVP (must-have) features?
- What are future / optional features?

---

## 3. Non-Functional Requirements

- How fast should the system be?
- How many users should it support?
- What is the expected scale?
- Do we need real-time features?
- Should we optimize for availability or consistency?

---

## 4. Data & Storage

- What data needs to be stored?
- Which database is suitable (SQL / NoSQL)?
- What is the data schema?
- How will we query the data efficiently?
- Do we need indexing?

---

## 5. API Design

- What APIs are needed?
- What are the main endpoints?
- What are request/response formats?
- How will authentication work?
- REST or event-based design?

---

## 6. High-Level Architecture

- What are the main components?
- Do we need frontend + backend separation?
- Do we need a load balancer?
- Do we need caching?
- Do we need message queues?

---

## 7. Data Flow

- What happens step-by-step for a user action?
- How does request move through the system?
- Where is data written and read?
- What happens on success and failure?

---

## 8. Scalability

- What happens if traffic increases 10x?
- What is the first bottleneck?
- Do we need multiple servers?
- Do we need horizontal scaling?
- What should be cached?

---

## 9. Reliability & Failure Handling

- What if database goes down?
- What if server crashes?
- What if network fails?
- Do we need retries?
- Do we need backups?

---

## 10. Security

- How do we authenticate users?
- How do we authorize actions?
- How do we protect APIs?
- Do we need rate limiting?
- Is data encrypted?

---

## 11. Optimization

- What can be cached?
- What can be precomputed?
- Can we reduce database load?
- Can we use async processing?
- Can we batch requests?

---

## 12. Trade-offs

- SQL vs NoSQL — why?
- Consistency vs availability?
- Performance vs cost?
- Simplicity vs scalability?

---

## 13. Future Improvements

- What features can be added later?
- How will system evolve?
- What breaks at scale?

---
