# 2 — Iteration 2: Refining Quality Attributes (Availability & Modifiability)

This iteration refines architectural mechanisms supporting **Availability (QA-2)** and **Modifiability (QA-5)** and finalizes the **Deployment View** introduced previously.

---

## 2.1 — Step 1: Review Inputs (Same as Iteration 1 — Step 1)

### **Design Purpose**
This is a greenfield system from a mature domain. The goal is to design a unified conversational interface to institutional data at Ontario Tech University, emphasizing **high availability**, **performance**, **security**, and **privacy**.

### **Primary Functional Requirements**
- **UC-1 — Access Academic Details**  
  Core business functionality, enabling personalized student information retrieval.

- **UC-2 — Receive Notifications**  
  Critical for timely user engagement and platform utility.

- **UC-5 — Regulate System Integrations**  
  Ensures secure, reliable communication with external institutional systems (LMS, Registration).

### **Quality Attribute Scenarios (Prioritized)**

| QA Attribute | Importance | Difficulty |
|-------------|------------|------------|
| **QA-1 Performance** | High | High |
| **QA-2 Availability** | High | High |
| **QA-3 Security** | High | High |
| **QA-4 Scalability** | High | Medium |
| **QA-5 Modifiability** | Medium | Medium |

### **Constraints**
- **CON-1:** Support ≥ 5,000 concurrent users  
- **CON-2:** Cross-platform (web + mobile) operation  
- **CON-3:** University-approved cloud deployment  
- **CON-4:** Privacy & compliance requirements  
- **CON-5:** Response time ≤ 2 seconds  
- **CON-6:** Unified AI backend for voice + text  

### **Architectural Concerns**
- **CRN-1:** Define microservice + integration structure  
- **CRN-2:** Leverage Python (FastAPI) + React  
- **CRN-3:** Secure handling of SSO + PII  
- **CRN-4:** Cloud scalability + auto-deployment  
- **CRN-5:** Simplify future AI model + API integrations  
- **CRN-6:** Clear module responsibilities  

---

## 2.2 — Step 2: Establish Iteration Goal by Selecting Drivers

Iteration 1 handled core structure and CRN-4 (scalability/deployment).  
Iteration 2 focuses on refining key remaining quality attributes.

### **Drivers Selected for Iteration 2**

| Driver | Reason for Inclusion | Status from Iteration 1 |
|--------|-----------------------|-------------------------|
| **QA-2 Availability (99.9%)** | Need concrete fault tolerance | Partially addressed |
| **QA-5 Modifiability** | Clean integration of new systems/models | Partially addressed |
| **CON-1 Concurrent Users (≥5000)** | Requires finalized deployment mapping | Partially addressed |
| **CRN-5 Future Integrations** | Standard interfaces required | Partially addressed |

### **Iteration Goal**
Refine architectural elements that enable **Availability** and **Modifiability**, and finalize deployment details required for **CON-1** and **CRN-5**.

---

## 2.3 — Step 3: Choose System Elements to Refine

### **Elements Selected**
- **Logic Tier (Microservice Cluster)**  
  Critical for QA-2: microservice failure must not interrupt service.

- **Integration Adapters Module**  
  Central for QA-5 and CRN-5.

- **API Gateway Routing & Health Check Paths**  
  Essential for availability + resilience.

- **Deployment Tier Mapping**  
  Needed to meet CON-1.

---

## 2.4 — Step 4: Choose Design Concepts to Satisfy Drivers

### **Design Decisions**

| Design Decision | Rationale |
|-----------------|-----------|
| **Active Redundancy for All Microservices** | Supports QA-2 uninterrupted service |
| **Heartbeat Monitoring + Auto-Recovery (Kubernetes/ECS)** | Enables rapid fault detection + 99.9% uptime |
| **Adapter Pattern + Information Hiding** | Supports QA-5 and CRN-5 future integrations |
| **Service Mesh/Internal Load Balancer** | Handles routing, failover, replication |
| **Unified Adapter Interface: `fetch(request: AIDAP_Request)`** | Stability across varying external APIs |

### **Discarded Alternatives**

| Alternative | Reason Rejected |
|------------|-----------------|
| **Passive Redundancy** | Failover too slow for QA-2 |
| **Direct Integration (No Adapters)** | Breaks modifiability; tight coupling |
| **Static Load Balancing Only** | Cannot handle failure-based rerouting |

---

## 2.5 — Step 5: Instantiate Elements, Allocate Responsibilities & Define Interfaces

### **Instantiation Decisions**

| Decision | Rationale |
|---------|-----------|
| **Create LMSAdapter, RegistrationAdapter, FutureAdapter Placeholders** | Supports QA-5 modularity and extensibility |
| **Define Canonical Adapter Interface** | Stable boundary across integrations |
| **Assign Health-Checks to Gateway + Orchestration Layer** | Early fault detection → QA-2 |
| **Instantiate Service Mesh / LB Between Gateway & Microservices** | Retry, circuit breaking, failover |
| **Refine Redis Cluster for Orchestration Caching** | Supports CON-1 performance under load |

Interfaces will be elaborated in future iterations.

---

## 2.6 — Step 6: Sketch Views & Record Design Decisions

Completed views for this iteration:
- **Module View for Integration Adapters**
- **Final Deployment View**
- **Sequence Diagram**

<img width="987" height="650" alt="image" src="https://github.com/user-attachments/assets/40f88539-bcfc-4a9e-b88b-0fd3817a0b19" />
<img width="1457" height="657" alt="image" src="https://github.com/user-attachments/assets/14e8e364-99a3-4335-bc38-e5e79c517129" />
<img width="1204" height="707" alt="image" src="https://github.com/user-attachments/assets/6c8a645b-caf0-4fed-bc4a-882d013cd9f8" />


---

## 2.7 — Step 7: Analyze Current Design & Review Iteration Goal Achievement

### **ADD Kanban-Style Progress Table**

| Driver | Not Addressed | Partially Addressed | Completely Addressed | Decisions Made |
|--------|---------------|----------------------|-----------------------|----------------|
| **QA-2 Availability** |  |  | ✓ | Active redundancy, heartbeats, mesh |
| **QA-5 Modifiability** |  |  | ✓ | Adapter Pattern + unified interface |
| **CON-1 Concurrent Users** |  |  | ✓ | Deployment clustering + LB |
| **QA-4 Scalability** |  |  | ✓ | Service mesh provides horizontal scaling |
| **QA-3 Security** | ✓ |  |  | Health-checks strengthen routing (full work later) |
| **CRN-5 Future Integrations** |  |  | ✓ | Clean adapter module design |
| **Remaining Functionalities (e.g., UC-3)** | ✓ |  |  | Deferred |

---

