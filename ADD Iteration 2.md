# Iteration 2

# Step 1: Review Inputs

## **Design Purpose**

This iteration refines the architecture created in Iteration 1 by introducing enhancements required to meet the performance, scalability, privacy, and maintainability requirements that were only partially addressed in the initial design. The improved design focuses on operational components such as caching, load balancing, monitoring, and model management.

## **Business Case**

As AIDAP grows to support more students, lecturers, and administrators, it must handle high load efficiently, maintain strict privacy standards, and allow maintainers to push updates without downtime. Iteration 2 ensures the system can support five thousand concurrent users, produce responses within two seconds, and provide reliable monitoring and maintainability for the university’s technical team.

## **Primary Functional Requirements (Iteration 2 Focus)**

The key functional drivers addressed in this iteration include:

* R1: Conversational access with improved response speed  
* R3: Enhanced integration stability with LMS, Registration, and Calendar  
* R5: Improved AI response handling and model performance  
* R7: Operational improvements for cloud scalability and uptime requirements  

### Use Cases

| ID | Description | Associated Requirement ID |
| :---- | :---- | :---- |
| UC-1: Retrieve lecture announcement | Must achieve faster response time with caching and routing improvements | R1, R3, R5, R6, RS1, RS10 |
| UC-2: View Class Analytics | Must improve query speed and reduce request load through caching and service scaling | R1, R3, R5, RL3, RL6, RL7 |
| UC-3: System Monitoring and Maintenance | Must provide visibility into system load, latency, errors, and allow updates with zero downtime | R7, RM1, RM2, RM4 |
| UC-4: Manage Notifications | Must improve reliability of event delivery with load balancing and more stable routing | R2, R4, RS2, RS6, RL4 |

### Quality Attribute Scenarios

| ID | Quality Attribute | Scenario | Associated Use Case |
| :---- | :---- | :---- | :---- |
| QA-1 | Performance | AIDAP must respond within two seconds even under heavy load through caching and load balancing | UC-1 |
| QA-2 | Privacy | Stronger access enforcement at the gateway and improved audit logging | UC-3 |
| QA-3 | Maintainability | AI models and backend services must be updatable without disrupting ongoing sessions | UC-3 |
| QA-4 | Availability/Scalability | AIDAP must use autoscaling and load balancing to sustain five thousand concurrent users | UC-1, UC-2, UC-3, UC-4 |
| QA-5 | Reliability | Notification and analytics services must remain stable even during external system failures | UC-4 |

### Constraints

| ID | Constraint |
| :---- | :---- |
| CON-1 | Must support five thousand concurrent users using scalable microservices |
| CON-2 | Must maintain 99.5 percent uptime with redundant deployments |
| CON-3 | Must strengthen SSO token validation at the API Gateway |
| CON-4 | Must improve backup and recovery processes with operational monitoring |
| CON-5 | Must remain cloud-native and support autoscaling |
| CON-6 | Must implement privacy controls including enhanced logging and secure model handling |

### Concerns

| ID | Concern |
| :---- | :---- |
| CRN-1 | Privacy protection must be strengthened through centralized authentication and logging |
| CRN-2 | Data integrity must be preserved when cached values differ from LMS data |
| CRN-3 | Authorization must be validated at a single, reliable entry point |
| CRN-4 | Response time must be consistently under two seconds during peak periods |
| CRN-5 | External integrations must be resilient to outages and slow responses |
| CRN-6 | AI model management must avoid performance regression or increased cost |

---

# Step 2: Establish Iteration Goal

## **Iteration Goal**

The goal of Iteration 2 is to enhance the architecture by improving performance, reliability, privacy, and maintainability. This includes introducing a distributed cache, load balancer, enhanced gateway, monitoring service, autoscaling capabilities, and a model management component.

## **Drivers Selected for Iteration 2**

### Functional Drivers:

* UC-1: Lecture announcement retrieval  
* UC-2: Class analytics retrieval  
* UC-3: Monitoring and maintenance  
* UC-4: Notification delivery  

### Quality Attribute Drivers:

* QA-1: Performance  
* QA-3: Maintainability  
* QA-4: Availability and Scalability  
* QA-5: Reliability  

### Constraint Drivers:

* CON-1: Concurrent user support  
* CON-2: Uptime requirement  
* CON-3: Enhanced security enforcement  
* CON-5: Cloud-native scalability  

---

# Step 3: Elements to Decompose

Iteration 2 focuses on decomposing operational and performance-critical server-side components to meet quality attribute requirements.

## **Element Selected for Decomposition**

AIDAP Backend Processing and Operational Layer

This includes the components responsible for routing, conversation handling, NLP, caching, model management, and monitoring.

---

# Step 4: Choose Design Concepts

### Distributed Cache Layer  
Improves performance for frequently accessed resources from LMS and registration systems.

### Enhanced API Gateway  
Adds centralized rate limiting, token validation, and request routing.

### Load Balancer  
Improves system performance, increases availability, and enables horizontal scaling.

### AI Model Manager  
Allows maintainers to switch, update, or roll back AI models without downtime.

### Monitoring and Logging Service  
Provides real time metrics, logs, and alerting for maintainers.

### Autoscaling Controller  
Responds to changes in system load by increasing or decreasing running service replicas.

---

# Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces

## Enhanced Elements Introduced in Iteration 2

### **1. API Gateway**
- Validates authentication tokens  
- Applies rate limits  
- Routes requests to appropriate services  
- Logs request metadata  

### **2. Load Balancer**
- Splits incoming traffic across multiple backend replicas  
- Provides failover support  

### **3. Cache Service**
- Stores frequently accessed announcements, analytics, and schedules  
- Reduces external API calls  

### **4. AI Model Manager**
- Manages model version control  
- Supports switching and rolling back models  

### **5. Monitoring and Logging**
- Collects latency, error, throughput, and operational metrics  
- Supports alerting  

### **6. Autoscaling Unit**
- Adds or removes backend replicas  
- Uses monitoring data to decide scaling actions  

---

## Interfaces

### **Client → Server**
- `/api/chat`  
- `/api/analytics`  
- `/api/notifications`  
- `/api/auth`  

### **Server → Cache**
- get entry  
- write entry  
- invalidate entry  

### **Server → Model Manager**
- fetch active model  
- switch model  

### **Monitoring Interfaces**
- log event  
- send alert  
- fetch metrics  

---

# Step 6: Sketch Views and Record Design Decisions

### Design Decisions Added in Iteration 2

* Introduced caching to support performance needs  
* Added load balancing and autoscaling for availability  
* Strengthened API Gateway to support security and privacy  
* Added AI Model Manager for maintainability  
* Added Monitoring and Logging to support operational visibility  
* Reduced dependency on external systems via caching and retry logic  

---

# Step 7: Analysis of Current Design

## **Driver Analysis Table**

| Driver | Not Addressed | Partially Addressed | Completely Addressed | Design Decisions Made |
| :---- | :---- | :---- | :---- | :---- |
| UC-1 Retrieve lecture announcement |  |  | ✔ | Caching and optimized routing improve performance |
| UC-2 View Class Analytics |  |  | ✔ | Faster queries from caching and scalable analytics processing |
| UC-3 Monitoring and Maintenance |  |  | ✔ | Monitoring dashboards and logs improve maintainability |
| UC-4 Manage Notifications |  | ✔ |  | Routing improved. Queueing enhancements still pending |
| QA-1 Performance |  |  | ✔ | Distributed caching reduces latency |
| QA-2 Privacy |  | ✔ |  | Gateway enforces better access control |
| QA-3 Maintainability |  |  | ✔ | Model Manager supports versioned updates |
| QA-4 Availability/Scalability |  |  | ✔ | Autoscaling and load balancing |
| CON-1 Five thousand users |  |  | ✔ | Horizontal scaling supports concurrency |
| CON-2 Uptime ninety nine point five percent |  | ✔ |  | Redundant deployments |
| CON-3 SSO authentication |  |  | ✔ | Gateway handles strong authentication |
| CON-4 Recovery |  | ✔ |  | Monitoring assists in tracking failures |
| CRN-1 Privacy compliance |  | ✔ |  | Access checks improved |
| CRN-2 Data integrity |  | ✔ |  | Cache invalidation rules still in refinement |
| CRN-3 Secure authorization |  |  | ✔ | Centralized gateway controls |
| CRN-4 AI response time |  |  | ✔ | Cache reduces load on NLP service |
| CRN-5 Integration complexity |  | ✔ |  | External adapters strengthened |
| CRN-6 AI cost management | ✔ |  |  | No finalized model optimization strategy |

