# Attribute-Driven Design (ADD) Iteration 3: Final Design Refinement

## Goal
To define the **Performance-enhancing mechanisms** and the detailed **Security architecture** to achieve **QA-1** and **QA-3**, and to document the core functional flow for **UC-2 (Receive Notifications)**, while simultaneously finalizing the necessary **QA-2 Availability tactics (Circuit Breaker, Observability)** to complete the design.

---

## 3.1 - Step 1 - Review Inputs
The inputs remain the set of architectural drivers established in the initial requirements analysis.  
The remaining high-priority drivers that must be addressed in this final iteration are:

| Driver ID | Type          | Description                                                                 | Priority (H/M/L) | Status after Iteration 2                                      |
|-----------|---------------|-----------------------------------------------------------------------------|------------------|---------------------------------------------------------------|
| QA-1      | Performance   | User-facing API calls must complete in ≤ 2 seconds under peak load.         | H                | Partially Addressed (Requires Caching/Protocol)               |
| QA-2      | Availability  | System uptime must be 99.9%.                                                | H                | Partially Addressed (Requires Fault Isolation/Verification)   |
| QA-3      | Security      | All PII must be encrypted at rest and in transit. User authentication must use SSO. | H                | Partially Addressed (Requires detailed SSO flow/Encryption)   |
| UC-2      | Functionality | Users must receive notifications (email, push) based on predefined criteria. | H                | Partially Addressed (Requires defining Service logic)         |
| CRN-6     | Constraint    | Module Responsibility Allocation for all services must be finalized.        | M                | Partially Addressed (Notification and Analytics responsibilities pending) |

---

## 3.2 - Step 2 - Establish Iteration Goal by Selecting Drivers
Iterations 1 and 2 successfully established the overall structure, deployment, and modifiability (**QA-5**).  
This iteration addresses the final high-risk drivers and the remaining core functional flow.

| Driver | Reason for Inclusion | Status from Iteration 2 |
|--------|----------------------|--------------------------|
| **QA-1 Performance (≤ 2 s)** | Requires definition of caching strategy and high-speed communication protocols to meet the hard performance constraint (CON-5). | Partially addressed (Structure supports it, tactics missing). |
| **QA-3 Security (PII & SSO)** | Requires detailed flow for SSO token validation, authorization, and secure PII handling (CRN-3). | Partially addressed (Dedicated service exists, flow missing). |
| **QA-2 Availability (99.9%)** | Requires the finalization of fault detection/isolation mechanisms (e.g., Circuit Breakers) and the full definition of monitoring/logging needed to verify the high availability target. | Partially addressed (Architecture is redundant, mechanisms for verification/isolation missing). |
| **UC-2 Receive Notifications** | The functional flow for this remaining core requirement must be defined. | Partially addressed (Dedicated service instantiated, flow missing). |
| **CRN-6 Module Responsibility Allocation** | Finalizing the Notification and Analytics Services is required to complete the allocation. | Partially addressed (High-level ownership defined, interfaces missing). |

---

## Iteration Goal
To define the **Performance-enhancing mechanisms** and the detailed **Security architecture** to achieve **QA-1** and **QA-3**, and to document the core functional flow for **UC-2 (Receive Notifications)**, while simultaneously finalizing the necessary **QA-2 Availability tactics (Circuit Breaker, Observability)** to complete the design.

## 3.3 - Step 3 - Choose Element(s) to Refine
The following elements require refinement to address the selected drivers:

- **Notification Service**: Needs responsibility allocation (CRN-6) and implementation of UC-2.  
- **Analytics Service**: Needs responsibility allocation (CRN-6) and implementation of data processing.  
- **API Gateway / Client Interface**: Needs security and performance mechanisms defined.  
- **Service-to-Service Communication Links**: Needs protocol selection for performance (QA-1) and security (QA-3).  

---

## 3.4 - Step 4 - Choose Design Concepts
We apply architectural patterns and tactics to address the selected quality attributes.

| Driver (QA)        | Tactic / Concept                                                                 | Rationale                                                                 |
|---------------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| **QA-1 Performance** | **Data Caching**: Client data is cached in-memory/Redis near the service consuming it (such as the API Gateway). | Reduces latency for repeated read requests, achieving the ≤ 2 seconds goal. |
| **QA-1 Performance** | **High-Speed Protocol (gRPC)**: Use gRPC for internal, service-to-service communication. | Provides faster, smaller payloads (Protocol Buffers) and persistent connections compared to REST/HTTP for synchronous needs. |
| **QA-3 Security**   | **Authentication/Authorization (JWT/OAuth2)**: The Auth Service issues a JWT after successful SSO via OAuth2. All internal services validate this token via the Gateway. | Enforces strong, standard-compliant security and role-based access control. |
| **QA-3 Security**   | **Encryption**: Enforce TLS 1.3 for all in-transit communication (Client-to-Gateway and Service-to-Service). Encrypt PII at rest in the database. | Satisfies the hard requirement for PII security. |
| **QA-2 Availability** | **Circuit Breaker**: Implement the Circuit Breaker pattern on services that call others (e.g., API Gateway calling downstream services). | Prevents cascading failures by isolating unhealthy services and providing fast failure. |
| **QA-2 Availability** | **Observability (Logging/Monitoring/Metrics)**: Implement distributed tracing, centralized logging (ELK stack/Prometheus), and standardized health checks. | Essential for monitoring the 99.9% target, detecting faults quickly, and allowing recovery (verification aspect of QA-2). |
| **UC-2 Functionality** | **Asynchronous Communication (Queue)**: The Notification Service consumes messages from the Message Queue (MQ) for processing and sending notifications. | Decouples the notification process from the triggering service, improving performance and availability of the primary request flow. |

---

## 3.5 - Step 5 - Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces
This step finalizes the system's structure by defining the last components and their contracts.

### A. Component and Connector Instantiation (Final)
We instantiate the final services and define their key interfaces:

| Component            | Responsibility (CRN-6)                                                                 | Interface/Contract                                                                 |
|----------------------|-----------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------|
| **Notification Service** | Handles all scheduled and real-time user communication (email, push, in-app).            | **Input**: Consumes `NotificationRequest` from Message Queue. <br> **Output**: External APIs (e.g., Email Service, Push Gateway). |
| **Analytics Service**    | Processes usage data, generates reports, and feeds metrics into the Monitoring system. | **Input**: Consumes `UsageEvent` from Message Queue. <br> **Output**: Metrics to Monitoring Service; Analytics data to its own Database. |
| **Cache Store (Redis)**  | Stores frequently accessed read-only user configuration data.                          | **Interface**: Standard Redis protocol (`GET/SET`). |

---

### B. Communication Definition
- **Client ←→ API Gateway**: HTTPS/REST with JWT attached (for Security QA-3).  
- **API Gateway ←→ Core Services**: gRPC for high-speed synchronous calls (for Performance QA-1).  
- **Services ←→ Notification/Analytics**: Message Queue (Async) for decoupling (for UC-2, Performance QA-1).  
- **Service Interfaces**: All internal service interfaces are defined using Protocol Buffers (for gRPC).  

---

## 3.6 - Step 6 - Sketch Views and Record Design Decisions
### A. Final Deployment Diagram
The final view includes all instantiated components, communication protocols, and the deployment of new elements (**Cache/Monitoring**).

<img width="1124" height="623" alt="image" src="https://github.com/user-attachments/assets/45ea431b-4be3-4358-8396-7d57a35bf809" />

