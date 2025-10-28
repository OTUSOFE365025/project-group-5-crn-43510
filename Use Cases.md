UC-1: Query Academic Info
A student communicates with AIDAP through text or voice to obtain academic or administrative information such as course schedules, upcoming exams, or grades.
The natural-language module interprets the query, maps it to structured requests, and retrieves relevant data from systems such as the LMS or registration database.
Personalized responses are generated using stored interaction history and contextual data.
This use case is continuous and supports multilingual operation across web, mobile, and voice channels.

UC-2: Receive Notifications
Students receive automated alerts related to deadlines, schedule changes, and institutional announcements.
The notification engine subscribes to event streams from LMS and calendar sources, filtering relevant updates for each authenticated student.
Notifications can be delivered through chat, email, or mobile push channels based on user preferences.
Students may modify notification frequency and preferred language through AIDAP’s settings.

UC-3: Manage Course Content
Lecturers use the assistant to create, upload, or update course materials.
Through conversational commands such as “Upload week-3 slides,” AIDAP connects to the LMS via secure APIs to store and index new content.
Access control verifies the lecturer’s identity and role before execution.
This use case streamlines course management by reducing manual portal navigation.

UC-4: View Analytics Dashboard
Lecturers and administrators can request analytical summaries (e.g., “Show class engagement for this week”).
The system aggregates performance, attendance, and usage data from institutional sources and renders graphical dashboards within the assistant interface.
Administrators can also view overall platform health and usage metrics.
This use case supports data-driven academic planning and operational decision making.

UC-5: Manage Integrations
Administrators configure and maintain the institutional integrations that enable AIDAP to access real-time data.
Through secure administrative commands or web interfaces, they add, update, or disable connections to LMS, registration, calendar, and email systems.
The assistant validates credentials, applies institutional security policies, and logs each configuration change for auditability.
This ensures consistent data synchronization across all connected services.

UC-6: Deploy and Monitor System
System maintainers oversee deployment and runtime monitoring of AIDAP’s cloud-native services.
They use an integrated dashboard to track system latency, error rates, and resource utilization, and can trigger zero-downtime updates through continuous-deployment pipelines.
The system automatically detects anomalies and notifies maintainers of failures, providing logs and rollback options to maintain high availability.
This use case ensures the reliability and performance of the AIDAP infrastructure.
