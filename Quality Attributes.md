## 4.2.2 Quality Attribute Scenarios — AIDAP

The following table lists the key quality attribute scenarios identified for the AI-Powered Digital Assistant Platform (AIDAP).  
Each scenario is described using the FCAPS format — *Source, Stimulus, Environment, Artifact, Response,* and *Response Measure* — and is linked to its associated use case(s).

---

| **ID** | **Attribute** | **Scenario** | **Associated Use Case** |
|:-------|:---------------|:--------------|:-------------------------|
| **QA-1** | **Performance** | **Source:** Student **Stimulus:** Submits a natural-language query **Environment:** Normal operation **Artifact:** NLP engine **Response:** The system generates and delivers a reply within 2 seconds **Response Measure:** ≤ 2 s latency | **UC-1** |
| **QA-2** | **Availability** | **Source:** User **Stimulus:** System node fails **Environment:** Operational mode **Artifact:** Cloud service cluster **Response:** Fail-over instance automatically activated and session resumed **Response Measure:** Recovery ≤ 30 s (99.5 % uptime) | **All** |
| **QA-3** | **Security** | **Source:** Unauthorized user **Stimulus:** Attempts system access **Environment:** Normal operation **Artifact:** Authentication module **Response:** Access denied and event logged **Response Measure:** 100 % of unauthorized attempts blocked and recorded | **UC-5** |
| **QA-4** | **Scalability** | **Source:** System load increase **Stimulus:** 5 000 concurrent users **Environment:** Peak usage period **Artifact:** Server cluster and load balancer **Response:** Instances auto-scale horizontally to maintain throughput **Response Measure:** Average latency ≤ 5 s under peak load | **All** |
| **QA-5** | **Modifiability** | **Source:** System maintainer **Stimulus:** Integrates a new AI model **Environment:** Design / development time **Artifact:** AI module architecture **Response:** New model added without changes to core services **Response Measure:** Integration completed within 2 developer days | **UC-6** |

---

> **Figure 4.2 – Quality Attribute Scenarios for AIDAP**  
> *(Each scenario follows the FCAPS six-part format to ensure quantifiable, testable non-functional requirements.)*
