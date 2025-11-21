# Iteration 2

# Step 1: Review Inputs

## **Purpose of This Iteration**

Iteration 2 focuses on refining the AIDAP system to improve performance, privacy, maintainability, scalability, and availability. This iteration introduces enhancements such as caching, load balancing, model version control, and monitoring, addressing partially completed drivers from Iteration 1.

## **Business Need**

AIDAP must function reliably at scale while supporting thousands of concurrent users and multiple integrations. Iteration 2 ensures the system can meet strict performance and availability requirements needed for real campus environments.

## **Updated Drivers for This Iteration**

### Functional Drivers:

* UC-1: Retrieve lecture announcement  
  Requires faster access paths and consistent performance.

* UC-2: View Class Analytics  
  Requires improved backend responsiveness and resilience.

* UC-3: System Monitoring and Maintenance  
  Requires real time operational visibility and zero downtime updates.

* UC-4: Manage Notifications  
  Requires more reliable event delivery pipelines.

### Quality Attribute Drivers:

* QA-1: Performance  
  Improve latency to consistently meet the two second requirement using caching and optimized request routing.

* QA-2: Privacy  
  Strengthen authentication, logging, and request validation across services.

* QA-3: Maintainability  
  Introduce version controlled AI models and reduce cross service dependencies.

* QA-4: Availability and Scalability  
  Ensure the system scales horizontally and remains available during peak load.

### Constraint Drivers:

* CON-1: Support five thousand concurrent users  
* CON-2: Ninety nine point five percent uptime  
* CON-3: University SSO integration  
* CON-4: Disaster recovery  
* CON-5: Cloud-native deployment  

---

# Step 2: Establish Iteration Goal

## **Iteration Goal**

The goal of Iteration 2 is to strengthen the architectural model by adding operational layers that improve system performance, availability, and maintainability. This is done through caching, load balancing, monitoring, and enhanced routing.

## **Drivers Selected for Iteration 2**

### Functional Drivers:
* UC-3 System Monitoring and Maintenance  
* UC-1 Retrieve Announcements  
* UC-2 View Analytics  

### Quality Attribute Drivers:
* QA-1 Performance  
* QA-3 Maintainability  
* QA-4 Availability and Scalability  

### Constraint Drivers:
* CON-1 Peak concurrency  
* CON-2 Uptime guarantee  
* CON-3 Stronger authentication handling  

---

# Step 3: Elements to Decompose

Iteration 2 decomposes the **AIDAP Backend Processing and Operational Services**, refining the system parts responsible for AI reasoning, routing, caching, and system monitoring.

## **Element Selected for Decomposition**

AIDAP Backend Processing Services

This includes routing, conversation handling, NLP, aggregation, and operational control.

---

# Step 4: Choose Design Concepts

To support Iteration 2 goals, these design concepts were selected:

### **One: Distributed Cache Layer**
Improves performance by storing frequently used LMS and analytics data to speed up repeated requests.

### **Two: API Gateway Enhancements**
Adds request throttling, token validation, and centralized routing rules.

### **Three: Load Balancer**
Distributes traffic across multiple backend replicas to maintain performance during peak periods.

### **Four: AI Model Manager**
Handles model versioning, updates, and rollbacks with zero downtime.

### **Five: Monitoring and Logging**
Provides dashboards for latency, throughput, error rates, and resource usage, supporting UC-3.

### **Six: Autoscaling**
Automatically adjusts service replicas based on demand.

---

# Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces

## **New or Enhanced Elements**

### **API Gateway**
- Enforces token validation
- Applies rate limits
- Routes requests to backend services
- Writes structured request logs

### **Load Balancer**
- Distributes traffic across backend nodes
- Handles failover when a node becomes unavailable

### **Cache Service**
- Stores LMS and calendar responses
- Ensures sub-two second user interactions
- Reduces external API load

### **AI Model Manager**
- Manages model versions
- Supports rolling upgrades and rollbacks
- Selects the most appropriate model for each request

### **Monitoring and Logging Service**
- Collects metrics such as latency, error frequency, and usage statistics
- Supports alerting for anomalies
- Provides dashboards for maintainers

### **Autoscaling Unit**
- Monitors resource usage
- Adds or removes service replicas automatically

---

## **Updated Interfaces**

### **Client → Gateway**
- Submit chat messages
- Request analytics
- Manage notifications
- Authenticate session tokens

### **Gateway → Backend Services**
- Route conversation requests
- Route analytics requests
- Enforce rate limits
- Block unauthorized requests

### **Backend Services → Cache**
- get(key)
- set(key, value)
- invalidate(key)

### **Backend Services → Model Manager**
- loadCurrentModel()
- switchModel(version)

### **Monitoring Interfaces**
- exportMetrics()
- logEvent()
- sendAlert()

---

# Step 6: Sketch Views and Record Design Decisions

## **Design Decisions Made in Iteration 2**

* Added caching to support performance scenarios  
* Introduced load balancing and autoscaling to support five thousand concurrent users  
* Enhanced API Gateway to improve privacy and access control  
* Added AI Model Manager to support maintainability and model version control  
* Added Monitoring and Logging to support UC-3 and privacy requirements  
* Strengthened boundaries between services for improved modifiability  
* Reduced reliance on external systems by caching and retry mechanisms  

---

# Step 7: Analysis of Current Design

## **Driver Analysis Table**

| Driver | Not Addressed | Partially Addressed | Completely Addressed | Design Decisions Made |
| :---- | :---- | :---- | :---- | :---- |
| UC-1 Retrieve lecture announcement |  |  | ✔ | Caching and load balancing provide faster data access. |
| UC-2 View Class Analytics |  |  | ✔ | Cached analytics and improved aggregation enhance speed. |
| UC-3 Monitoring and Maintenance |  |  | ✔ | Monitoring dashboards, logs, and metrics added. |
| UC-4 Manage Notifications |  | ✔ |  | Notification routing improved. Queue refinement pending. |
| QA-1 Performance |  |  | ✔ | Cache layer improves latency significantly. |
| QA-2 Privacy |  | ✔ |  | Stronger routing control added at gateway. Full encryption design pending. |
| QA-3 Maintainability |  |  | ✔ | Model Manager allows zero downtime model updates. |
| QA-4 Availability and Scalability |  |  | ✔ | Load balancing, autoscaling, and redundancy implemented. |
| CON-1 Five thousand users |  |  | ✔ | Horizontal scaling supports peak periods. |
| CON-2 Ninety nine point five percent uptime |  | ✔ |  | Redundant nodes provide stability. Disaster recovery procedures still in progress. |
| CON-3 SSO authentication |  |  | ✔ | Gateway consolidates token enforcement. |
| CON-4 Backup and recovery |  | ✔ |  | Backup defined, recovery automation pending. |
| CRN-1 Privacy compliance |  | ✔ |  | Logging and access enforcement support compliance. |
| CRN-2 Data integrity |  | ✔ |  | Cache invalidation needs additional refinement. |
| CRN-3 Secure authorization |  |  | ✔ | Gateway and identity service maintain secure access. |
| CRN-4 AI response time |  |  | ✔ | Cache and routing improvements maintain the two second requirement. |
| CRN-5 Integration complexity |  | ✔ |  | Adapters and caching help reduce dependency impact. |
| CRN-6 AI cost management | ✔ |  |  | No final model optimization strategy defined. |

