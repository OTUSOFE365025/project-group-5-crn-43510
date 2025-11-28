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
