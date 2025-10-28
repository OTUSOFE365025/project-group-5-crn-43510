## 4.2.3 System Constraints — AIDAP

The following constraints outline the key technical and operational boundaries within which the **AI-Powered Digital Assistant Platform (AIDAP)** must function.  
These limitations shape the system’s architecture and ensure that AIDAP remains scalable, secure, and reliable while meeting the needs of all university stakeholders.

---

| **ID** | **Constraint** | **Description** |
|---------|----------------|-----------------|
| **CON-1** | **Scalability Requirement** | AIDAP must be capable of supporting at least **5,000 users at the same time**. This ensures that even during busy academic periods such as course registration or final exams the system remains responsive and stable. The architecture should allow for easy horizontal scaling to handle future growth. |
| **CON-2** | **Cross-Platform Access** | The platform should work seamlessly across **modern web and mobile browsers**, as well as approved university mobile apps. This guarantees that students, faculty, and staff can access the assistant from any device whether it’s a laptop, tablet, or smartphone without technical barriers. |
| **CON-3** | **Cloud Deployment Environment** | AIDAP will be hosted on a **university-approved cloud service** such as Azure or AWS Education Tier. Using a secure cloud environment ensures reliable performance, automated deployment, and strong protection of institutional data through network isolation and containerized microservices. |
| **CON-4** | **Privacy and Compliance** | Since AIDAP deals with sensitive academic and personal data, all information handling must strictly follow **Ontario Tech’s privacy and retention policies**, as well as **PIPEDA** standards. User interactions and logs should be anonymized, encrypted, and stored only for the approved duration. |
| **CON-5** | **Performance Target** | To provide a smooth user experience, the system should respond to most queries in **under two seconds**. This response time includes processing the natural language input, retrieving information, and generating a clear, conversational reply to the user. |
| **CON-6** | **Availability Objective** | The platform must achieve at least **99.5% uptime each month**. Built-in fail-over and backup systems will ensure that AIDAP remains available even during maintenance or unexpected technical issues, minimizing disruption to users. |
| **CON-7** | **Unified AI Backend Models** | Both the **voice and text interfaces** should rely on the same underlying AI models and data sources. This keeps responses consistent across platforms, ensuring that users receive the same quality of information no matter how they interact with the assistant. |

---

> **Figure 4.2 – System Constraints for AIDAP**  
> *(These constraints establish the foundation for performance, security, and scalability decisions that will influence the architecture of the system.)*
