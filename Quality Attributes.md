## Quality Attribute Scenarios — AIDAP

The following table lists the key quality attribute scenarios identified for the **AI-Powered Digital Assistant Platform (AIDAP)**. Each scenario is described using the **FCAPS** format — *Source, Stimulus, Environment, Artifact, Response,* and *Response Measure* — and is linked to its associated use case(s).

---

| **ID** | **Attribute** | **Scenario** | **Associated Use Case** |
|:-------|:---------------|:--------------|:-------------------------|
| **QA-1** | **Performance** | **Source:** Student<br>**Stimulus:** Submits a natural-language query<br>**Environment:** Normal operation<br>**Artifact:** NLP engine<br>**Response:** The system generates and delivers a reply within 2 seconds<br>**Response Measure:** $\leq 2$ s latency | **UC-1** |
| **QA-2** | **Availability** | **Source:** User<br>**Stimulus:** System node fails<br>**Environment:** Operational mode<br>**Artifact:** Cloud service cluster<br>**Response:** Fail-over instance automatically activated and session resumed<br>**Response Measure:** Recovery $\leq 30$ s ($99.5$ % uptime) | **All** |
| **QA-3** | **Security** | **Source:** Unauthorized user<br>**Stimulus:** Attempts system access<br>**Environment:** Normal operation<br>**Artifact:** Authentication module<br>**Response:** Access denied and event logged<br>**Response Measure:** $100$ % of unauthorized attempts blocked and recorded | **UC-5** |
| **QA-4** | **Scalability** | **Source:** System load increase<br>**Stimulus:** $5,000$ concurrent users<br>**Environment:** Peak usage period<br>**Artifact:** Server cluster and load balancer<br>**Response:** Instances auto-scale horizontally to maintain throughput<br>**Response Measure:** Average latency $\leq 5$ s under peak load | **All** |
| **QA-5** | **Modifiability** | **Source:** System maintainer<br>**Stimulus:** Integrates a new AI model<br>**Environment:** Design / development time<br>**Artifact:** AI module architecture<br>**Response:** New model added without changes to core services<br>**Response Measure:** Integration completed within $2$ developer days | **UC-6** |

---
