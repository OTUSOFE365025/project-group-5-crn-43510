## 4.2.3 System Constraints — AIDAP

The following constraints define the technical and operational boundaries under which the **AI-Powered Digital Assistant Platform (AIDAP)** must operate.  
These constraints guide architectural decisions and ensure compliance with institutional requirements for scalability, reliability, and security.

| **ID** | **Constraint** | **Description** |
|---------|----------------|-----------------|
| **CON-1** | **Scalability Requirement** | The system shall support a minimum of 5 000 concurrent users under normal operating conditions. This limit reflects expected peak university usage during registration or examination periods and defines baseline capacity for horizontal scaling and load balancing. |
| **CON-2** | **Cross-Platform Access** | AIDAP must be accessible through modern web and mobile browsers (Chrome v100+, Firefox v95+, Safari 15+, Edge 100+) and through approved mobile apps. Browser compatibility ensures accessibility for students and staff across Windows, macOS, Android, and iOS platforms. |
| **CON-3** | **Cloud Deployment Environment** | The system shall be deployed on a university-approved cloud platform (e.g., Azure or AWS Education Tier). The cloud environment must support containerized microservices, continuous deployment pipelines, and secure network isolation (VPC/subnets). |
| **CON-4** | **Privacy and Compliance** | All data handling must comply with institutional privacy and data-retention policies, including PIPEDA and Ontario Tech University security standards. User interactions, logs, and analytics data must be anonymized and retained only for approved durations. |
| **CON-5** | **Performance Target** | Under normal load, the assistant shall generate responses within 2 seconds for 90 % of queries. This latency target includes natural-language processing, data retrieval, and response rendering to ensure real-time conversational interaction. |
| **CON-6** | **Availability Objective** | The system shall maintain 99.5 % monthly availability, including fail-over and backup recovery mechanisms. Automatic replication and health monitoring must be implemented to minimize downtime during maintenance or component failure. |
| **CON-7** | **Unified AI Backend Models** | Both text and voice interfaces shall utilize the same backend AI models and data sources to guarantee consistency in responses. This constraint ensures that updates to the language model or knowledge base propagate uniformly across modalities. |
