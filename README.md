# SOFE3650F25-Project
SOFE3650F25 Project Repository for Group Number: 5

## Group Members:
- Name: Eesha Razia | Student ID: 100930229
- Deliverable 1 Contribution: Use Case models, Quality Attributes, Business Case
- Deliverable 2 Contribution: ADD Iteration 2

- Name: Sayyeda Faruqui | Student ID: 100912573
- Deliverable 1 Contribution: System Constraints, Architectural Concerns, Business Case
- Deliverable 2 Contribution: ADD Iteration 1


## Deliverable 1: Requirements Analysis

Includes Architectural Drivers (derived from the given requirements):
- Use Case models
- Quality Attributes
- System Constraints 
- Architectural Concerns
- Business Case

#### Note: All tables used in the markdown files of Deliverable 1 were generated using the following resource: https://www.tablesgenerator.com/markdown_tables in order to follow the ADD FCAPS Case Study Formatting.

## Deliverable 2: ADD Iteration 1 and Iteration 2

#### Note: All tables used in the markdown files of Deliverable 2 were generated using the following resource: https://www.tablesgenerator.com/markdown_tables in order to follow the ADD FCAPS Case Study Formatting.

## Deliverable 3:ATAM Utility Tree and Risk Assessment
# ATAM Evaluation for AIDAP (AI Digital Assistant Platform)

## 1. Introduction to ATAM for AIDAP

The Architectural Trade-off Analysis Method (ATAM) is used to evaluate how well the AIDAP system’s architecture satisfies its critical quality attributes. ATAM focuses on:

- Performance  
- Availability / Reliability  
- Security  
- Modifiability  

AIDAP’s architecture was designed using ADD (Iterations 1–3). ATAM is used here to analyze risks, sensitivity points, and tradeoffs related to those design decisions.

---

## 2. Business Drivers (ATAM Step 2)

### Primary Functional Drivers
- UC-1: Access Academic Details  
- UC-2: Receive Notifications  
- UC-5: Regulate System Integrations  

### Quality Attribute Drivers
- Performance (QA-1): Response time ≤ 2 seconds  
- Availability (QA-2): 99.9% uptime, failover ≤ 30 seconds  
- Security (QA-3): SSO + encrypted PII  
- Scalability (QA-4): ≥ 5,000 concurrent users  
- Modifiability (QA-5): Add new APIs / AI models easily  

### Constraints
- Cloud deployment (Azure/AWS)  
- Use Python FastAPI + React SPA  
- Use institutional SSO  
- Unified AI backend  

---

## 3. Architectural Approaches (ATAM Step 4)

Architectural decisions central to AIDAP:

- Microservice Architecture  
- API Gateway + NLP Core  
- Service Mesh + Kubernetes Auto-Scaling  
- Adapter Pattern for External Systems  
- React SPA Client-Side Application  
- Redis Caching Layer  
- gRPC Internal Communication  
- Layered Security Model + SSO (OAuth2/JWT)  
- Circuit Breaker Pattern  
- Centralized Monitoring / Observability  

---

## 4. ATAM Utility Tree (ATAM Step 5)

### Top-Level Utility Goal: AIDAP Overall System Utility

---

### 1. Performance (High Importance, High Difficulty)

#### 1.1 Use-Case Scenario: Peak Query Response
- Stimulus: 5,000 users request academic details simultaneously  
- Environment: Peak load  
- Response: System replies ≤ 2 seconds  
- Measure: 95th percentile response time  

#### 1.2 Growth Scenario: Caching Reuse
- Stimulus: User repeats a prior query  
- Environment: Cache warm  
- Response: Serve data from Redis cache  
- Measure: Response ≤ 500 ms  

---

### 2. Availability (High Importance, High Difficulty)

#### 2.1 Exploratory Scenario: Microservice Crash
- Stimulus: NLP Core container crashes  
- Environment: Normal operation  
- Response: Service mesh routes traffic to replica  
- Measure: Failover ≤ 30 seconds, zero dropped sessions  

#### 2.2 Stress Scenario: External API Failure
- Stimulus: LMS API becomes unresponsive  
- Response: Circuit breaker activates; system returns cached or partial information  
- Measure: System remains available  

---

### 3. Security (High Importance, High Difficulty)

#### 3.1 Exploratory Scenario: Invalid Token
- Stimulus: Tampered or expired JWT  
- Response: API Gateway blocks request and logs event  
- Measure: 100 percent blocked  

#### 3.2 Use-Case Scenario: Secure Data Transfer
- Stimulus: User requests personal academic record  
- Response: All data encrypted via TLS 1.3; PII encrypted at rest  
- Measure: No plaintext exposure  

---

### 4. Scalability (High Importance, Medium Difficulty)

#### 4.1 Growth Scenario: Enrollment Week Surge
- Stimulus: Traffic spikes by factor of three  
- Response: Auto-scale new pods in cluster  
- Measure: Zero downtime; performance maintained  

---

### 5. Modifiability (Medium Importance, Medium Difficulty)

#### 5.1 Growth Scenario: Integrating a New External System
- Stimulus: Add Library System API  
- Response: Implement new adapter using unified `fetch(request)` interface  
- Measure: ≤ 3 engineer-days, no changes to other services  

#### 5.2 Exploratory Scenario: Update AI Model
- Stimulus: Replace NLP backend  
- Response: Only NLP Core changes; other services unaffected  
- Measure: No system downtime  

---

## 5. ATAM Risk Assessment (Step 6)

### ATAM Risk, Sensitivity, and Tradeoff Table

| Architectural Decision | Risk (R) | Sensitivity Point (S) | Tradeoff (T) |
|------------------------|----------|-------------------------|--------------|
| Microservice Architecture | Operational complexity may cause misconfigured deployments | System performance highly sensitive to inter-service latency | More scalability but higher overhead compared to monolith |
| API Gateway as Single Entry | Gateway overload may bottleneck system | Performance depends on gateway throughput | Strong security centralization vs. single bottleneck risk |
| Service Mesh (Istio/Linkerd) | Incorrect routing or circuit-breaker config can cause outages | Availability depends on rapid health checks | Higher reliability vs. more operational cost |
| Redis Caching Layer | Stale data may cause outdated responses | Performance sensitive to cache hit rate | Fast responses vs. risk of stale data |
| Adapter Pattern | API schema changes may break adapters | Modifiability depends on unified `fetch()` interface | Clean separation vs. additional abstraction cost |
| Circuit Breaker | Aggressive settings may block healthy services | Availability depends on threshold configuration | High resilience vs. potential false blocking |
| gRPC Internal Calls | More difficult to debug compared to REST | Serialization overhead affects latency | Higher performance vs. developer complexity |
| OAuth2/JWT SSO | Incorrect token expiry may break sessions | Security sensitive to token validation logic | Higher security vs. reduced usability |
| Kubernetes Auto-Scaling | Incorrect CPU or memory thresholds may cause slow scaling | Availability depends on correct metrics | High scalability vs. increased cloud cost |
| Encrypted Database | Encryption slows read/write operations | Security sensitive to encryption key rotation | Strong security vs. slight performance cost |

---

## 6. Risk Themes (ATAM Step 9 Summary)

From the ATAM evaluation, the major architectural risk themes for AIDAP are:

1. Performance is highly dependent on caching effectiveness and low inter-service latency.  
2. Availability relies heavily on correct service mesh and auto-scaling configuration.  
3. Security is sensitive to correct SSO token validation and encryption key management.  
4. Modifiability depends on strict adherence to the adapter interface (`fetch()`).  
5. Tradeoff exists between strong security mechanisms and performance overhead.

---

## 7. Final ATAM Conclusion

The ATAM evaluation demonstrates that the AIDAP architecture is robust and aligned with the project’s quality attribute drivers. Performance, availability, and security are strongly supported through microservices, caching, circuit breakers, service mesh routing, and layered security. The adapter pattern cleanly supports modifiability and future integrations.

Risks identified mainly configuration sensitivity, caching consistency, and token management—are manageable and can be mitigated with monitoring, automated testing, and well-defined operational procedures.

Overall, the architecture satisfies the quality goals and provides a scalable, secure foundation for implementation.


