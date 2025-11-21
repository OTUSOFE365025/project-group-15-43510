# Iteration 1

# Step 1: Review Inputs

## **Design Purpose**

This is a greenfield design for the AI-Powered Digital Assistant Platform (AIDAP). This is a new system to be created from scratch to address inefficiencies within current university systems.  
---

## **Business Case**

The current university systems in place are very disconnected and inefficient at relaying information outward. Communication is mostly done through LMS, Emails, and Web portals, which can be very time consuming for quick questions and great concerns. A fix to this problem would be the implementation of an AI-Powered Digital Assistant Platform (AIDAP).  
AIDAP fixes this problem by giving users a unified, quick and interactive interface by leveraging the power of AI. By using an AIDAP, we can query results using natural human language and have direct answers to our queries through voice and text. By integrating our AIDAP to existing University systems in place, we can streamline access to courses, grades, deadlines, schedules and announcements, allowing everyone in the university to save time and energy. The platform architecture ensures that the system will be scalable, highly available and reliable, allowing it to reach thousands of students while maintaining its security and functionality.

## **Primary Functional Requirements**

The key functional drivers for the architecture

* R1: Conversational access to institutional data and services  
* R3: Integration with existing data sources (LMS, Registration System, Calendars)  
* R4: Support both text and voice interaction modes  
* R5: Use AI models to interpret natural language queries  
* R6: Generate responses using both stored knowledge and live data  
* R7: Deployable as a cloud-native, scalable service

### Use Cases

| ID | Description | Associated Requirement ID |
| :---- | :---- | :---- |
| UC-1: Retrive lecture annoncement | A student interacts with AIDAP to learn about any new announcements from their lecture. The system returns the announcements to the student | R1, R3, R5, R6, RS1, RS2, RS8, RS9, RS10 |
| UC-2: View Class Analytics | A lecturer asks AIDAP for a summary of student performance, like average grade, attendance, and engagement. AIDAP retrieves and aggregates data from the LMS to present analytics. | R1, R3, R5, RL3, RL6, RL7 |
| UC-3: System Monitoring and Maintenance | The system maintainer monitors the latency, errors and model performance via dashboards and allows deployments of updates with zero downtime. | R7, RM1, RM2, RM4 |
| UC-4: Manage Notifications | A student or lecturer configures and receives notifications for deadlines, announcements, and events through text or voice. AIDAP delivers personalised updates via user-controlled preferences. | R2, R4, RS2, RS6, RL4 |

### Quality Attribute Scenarios

| ID | Quality Attribute | Scenario | Associated Use Case |
| :---- | :---- | :---- | :---- |
| QA-1 | Performance | AIDAP should respond to the user within 2 seconds under any conditions to ensure the conversation is seamless. (RS10) | UC-1 |
| QA-2 | Privacy | AIDAP should conform to university privacy policies and not disperse private data. (RA2, RA5, R8) | UC-3 |
| QA-3 | Maintainability | Allowing maintainers to update models, APIs, and configurations without downtime (RM1) | UC-3 |
| QA-4 | Availability/Scalability | AIDAP must remain available 99.5% of the time per month (RS11) and handle up to 5000 concurrent users without performance degradation (RA7) | UC-1, UC-2, UC-3, UC-4 |
| QA-5 | Usability | When a new user interacts with AIDAP, the interface guides them intuitively using conversational cues and context-aware responses. (RS12) | UC-4 |

### Constraints

| ID | Constraint |
| :---- | :---- |
| CON-1 | Must handle up to 5000 concurrent users. (RA7) |
| CON-2 | Must be available to use 99.5% time per month. (RS11, RA6) |
| CON-3 | Must use the institution’s Single Sign-On system. (RS7) |
| CON-4 | Must perform automatic backups and support disaster recovery. (RA6, RM6) |
| CON-5 | Must be deployable as a cloud-native service. (R7) |
| CON-6 | Must comply with data retention and encryption standards (R8, RA2, RA5) |

Concerns

| ID | Concern |
| :---- | :---- |
| CRN-1 | Protecting User data and privacy through communication with AI to comply with school regulations. |
| CRN-2 | The system must preserve data integrity across all platforms when accessing data |
| CRN-3 | Require a secure authorisation for some data to prevent classified information from being leaked. |
| CRN-4 | Allowing the AI to not take longer than 2 seconds to come up with a response to maintain efficiency. |
| CRN-5 | Integration complexity with multiple external systems (LMS, Registration, Calendar, Email) requires robust error handling and fallback mechanisms. |
| CRN-6 | AI model selection and cost management \- need to balance model performance, latency, and operational costs. |

---

# Step 2: Establish Iteration Goal

## **Iteration Goal**

Establish the overall system structure for AIDAP that:

* Supports user interaction for students, faculty, and administrators (UC-1, UC-2, UC-4)  
* Enables continuous deployment of system updates and AI model improvements without service interruption (UC-3)  
* Implements secure access control using SSO with appropriate safeguards  
* Implements cloud-based deployment architecture with scalable components to handle peak usage  
* Maintains separation between presentation, business, and data layers to enable independent updates

## 

## **Drivers Selected for Iteration 1:**

### Functional Drivers:

* UC-1: Retrieve lecture announcement  
  Core student-facing interaction which requires fast response times and reliable data access.  
* UC-2: View Class Analytics  
  Requires LMS integration, authentication, authorisation, and consistent API communication.  
* UC-3: System Monitoring and Maintenance  
  High architectural impact due to modifiability and the requirement for zero downtime.  
* UC-4: Manage Notifications  
  Requires event-driven architecture and personalised delivery mechanisms.

### Quality Attribute Drivers:

* QA-1: Performance  
  Caching requires a 2-second response time, API design, and component interaction patterns.  
* QA-2: Privacy  
  Compliance requirements affecting data handling, logging, access control, encryption, and component isolation.  
* QA-3: Modifiability  
  Business and technical priority driving modular design, clear boundaries, deployment automation, and component independence.  
* QA-4: Availability/Scalability  
  Registration and exam periods require redundancy, scalability, load balancing, and fault tolerance.

### Constraint Drivers:

* CON-1: 5000 Concurrent users  
  Determines service replication strategy, load balancing approach, resource allocation, and infrastructure sizing decisions.  
* CON-2: 99.5% uptime per month  
  Influences redundancy design, failover mechanisms, monitoring requirements, and deployment architecture to minimise downtime.  
* CON-3: University SSO authentication  
  Dictates authentication approach and influences security architecture across system boundaries.  
    
* CON-4: Automatic backups and data recovery  
  Affects database selection, storage architecture, backup automation requirements, and recovery procedure design.  
* CON-5: Cloud-native deployment  
  Determines deployment technologies, container orchestration, and infrastructure automation approaches.  
* CON-6: Data retention and encryption standards  
  Influences data storage design, backup procedures, encryption implementation, and lifecycle management.

---

# Step 3: Elements to decompose

For iteration 1, the system is treated as a single architectural element

## **Element Selected for Decomposition**

AIDAP System (Complete System)

The goal of this iteration is to establish the overall structure of the AIDAP system. This means the system as a whole is selected for initial decomposition into major subsystems and layers

---

# Step 4: Choose Design Concepts

## **Architectural Design Concepts Selected**

* Logical Architecture Pattern: Layered Architecture (Presentation, Business, Data)  
* Service Architecture Style: Service-Oriented Architecture with RESTful and GraphQL interfaces  
* Client Application Style: Rich Client Application with local processing capabilities  
* Deployment Architecture: Cloud-native Multi-Tier Deployment with Container Orchestration  
* Supporting Patterns:  
  * Gateway Aggregation Pattern  
  * Modular AI Processing Subsystem  
  * Identity Federation  
  * Role-Based Access Control  
  * Publish-Subscribe Messaging  
  * Distributed Caching

| Design Decision | Rationale |
| :---- | :---- |
| Adopt a Layered Architecture for logical system Organization | Layered architecture provides clear separation between user interface, business processing, and data access responsibilities. This separation directly supports QA-3 by allowing changes to AI models, external integrations, and user interfaces to occur independently from each other. The pattern supports QA-5 by isolating presentation concerns, making interface improvements easier. It addresses CON-6 by restricting sensitive data operations to lower layers with appropriate controls. The layered approach also facilitates CRN-2 by establishing clear data flow and validation boundaries. |
| Implement a Cloud-Native Multi-Tier deployment architecture | Multi-tier cloud deployment directly addresses QA-4 through elastic infrastructure, automatic scaling, and geographic distribution capabilities. This satisfies CON-5 which calls for cloud-native deployment, and supports CON-4 through cloud provider backup and disaster recovery services. The tiered structure enables independent scaling of presentation, application, and data components. Cloud deployment also supports CRN-5 by providing managed services for complex integration scenarios. |
| Structure backend as Service-Oriented Architecture | Service-oriented design exposes system capabilities through well-defined API contracts consumed by various clients. This directly supports R4 and enables different client types to access the same services. The approach aligns with QA-1 by enabling targeted optimization of individual services. It supports QA-2 by centralizing authentication, authorization, and audit logging at service boundaries. Service orientation facilitates QA-3 through loose coupling between services. |
| Create a Modular AI Processing Subsystem | Separating AI processing into an independent subsystem allows AI models and processing logic to evolve without affecting other system components, directly addressing QA-3 and CRN-6. This modularity supports UC-3 by enabling AI model updates to be deployed independently. The design allows for multiple AI providers or models to be utilized based on query type, addressing cost and performance optimization. Isolation also helps manage CRN-4 by making AI processing time measurable and optimizable. |
| Integrate institutional SSO with Role-Based Access Control | SSO integration satisfies CON-3 by leveraging existing institutional identity infrastructure. RBAC implementation addresses QA-2 and CRN-3 by ensuring users can only access data appropriate to their role (student, faculty, administrator). This combined approach centralizes authentication logic, simplifying security maintenance and audit compliance. The design supports all use cases by providing appropriate access controls for different user types. |
| Design client applications using Rich Client Application pattern | Rich client architecture enables responsive, interactive user experiences by performing local processing, caching, and state management. This approach supports QA-1by reducing server round-trips and enabling optimistic UI updates. The pattern enhances QA-5 through smooth conversational flows and immediate feedback. Rich clients can maintain user context and preferences locally while communicating with backend services via standard APIs, supporting R4 (multiple interaction modes). This design accommodates web browsers, native mobile applications, and voice interface adaptations. |
| Implement Event-Driven architecture for notifications | Event-driven design decouples notification generation from delivery, supporting UC-4 and enabling asynchronous processing. This approach improves QA-4 by preventing notification processing from blocking user interactions. Events can be routed to multiple handlers (email, SMS, push notifications) without coupling notification sources to delivery mechanisms. The pattern supports QA-3 by allowing new notification channels to be added without modifying existing components. |
| Deploy distributed caching layer | Caching frequently accessed data (course schedules, common queries, user sessions) directly addresses QA-1 by reducing database load and external API calls. Cache implementation helps meet the 2-second response requirement for common queries. The design includes cache invalidation strategies to balance performance with data freshness, addressing CRN-2 Data Integrity. Distributed caching also supports QA-4 by distributing load across cache nodes. |

---

# Step 5: Instantiate Architectural Elements, Allocate Responsibilities, and Define Interfaces

## **Architectural Element Instantiation Decisions**

| Design Decision and Location | Rationale |
| :---- | :---- |
| Introduce API Gateway as a single entry point for all client requests | The API Gateway centralizes cross-cutting concerns including authentication verification, request routing, rate limiting, and API versioning. This design supports CON-3 by providing a single point for authentication enforcement and QA-2 by centralizing access control. The gateway pattern also improves QA-3 by decoupling clients from backend service topology changes. |
| Seperate Natural Language Processing for Conversation Orchestration Service | Isolating AI and NLP processing into a dedicated service allows AI models and processing logic to be updated independently without affecting conversation flow management, directly satisfying QA-3 and CRN-6. This separation supports UC-3 and enables different AI models to be selected based on query complexity, addressing CRN-4 |
| Create Data Aggregation Service with external system adapters | A dedicated integration service with adapter pattern for each external system isolates dependencies and provides a unified data access interface. This directly addresses CRN-5 by centralizing error handling, retry logic, and circuit breakers. The abstraction supports QA-3 when external APIs change and enables QA-1 through coordinated caching strategies. |
| Implement distributed caching layer between application services and data sources | Multi-level caching directly addresses QA-1 by reducing database queries and external API calls to meet the 2-second response requirement. Cache placement at the Data Aggregation Service level enables sharing cached data across multiple application services, improving QA-4. TTL-based invalidation balances performance with data freshness concerns (CRN-2). |
| Deploy Event Management Service with asynchronous message queue | Decoupling notification generation from delivery through a message broker supports UC-4 while enabling asynchronous processing that improves QA-4. Events can be published once and consumed by multiple handlers (email, SMS, push) without coupling, supporting QA-3 when adding new notification channels. The queue also provides delivery guarantees and retry capabilities. |
| Establish Identity and Access Service Integrating with Institutional SSO | A dedicated authentication service satisfies CON-3 and provides a single point for implementing QA-2 and CRN-3. Token-based session management enables stateless authentication across distributed services. RBAC implementation within this service ensures consistent authorization decisions and simplifies audit logging for compliance. |
| Structure Client application using Rich Client pattern with local business logic | Rich client architecture enables responsive user experience by performing validation, preprocessing, and optimistic UI updates locally, supporting QA-1 and QA-5. Local processing reduces server round trips while maintaining security by keeping sensitive operations server-side. The pattern supports multiple client types like web, mobile, voice through standardized backend APIs, supporting R4. |
| Seperate Conversation Orchestration from domain services | The Conversation Orchestration Service coordinates between NLP processing, data retrieval, and response generation without implementing domain-specific logic. This separation supports QA-3 by allowing business rules to evolve independently from conversation flow. The orchestrator maintains conversation context and state, enabling multi-turn interactions for UC-1 and UC-4 while keeping domain logic reusable across different interaction patterns. |

## **Major Architectural Components**

### Client-Side Components

| Component | Responsibility |
| :---- | :---- |
| User Interface Components | Render conversational interface elements, display academic information dashboards, capture user input through text/voice, present system responses with appropriate formatting, manage visual layout and navigation. Support QA-5 through intuitive conversational design. |
| Interaction Controllers | Coordinate user interactions and conversation flow, manage conversation state and context locally, coordinate between UI components and server communication module, handle navigation, implement client-side validation, manage error display and user feedback. |
| Server Communication Module | Abstract all backend communication details from other client components, format API requests according to server contracts, parse and transform API responses for client consumption, implement request retry logic with exponential backoff, manage connection state and network error handling gracefully. |
| Local Cache Store | Maintain temporary cache of recent conversations and responses, store user preferences and settings locally, cache frequently accessed reference data (course lists, schedules), support offline degradation for limited functionality. Improves QA-1 (Performance) through reduced server calls. |

### Admin-Side Components

| Component | Responsibility |
| :---- | :---- |
| API Gateway | Serve as single entry point for all client requests, route requests to appropriate backend services based on API paths, verify authentication tokens and enforce session validity, implement rate limiting per user and per service, perform request schema validation, aggregate responses from multiple services when needed, manage API versioning and request transformation. Critical for CON-3 and QA-2. |
| Identity and Access Service | Integrate with institutional SSO system using OAuth or SAML protocols, validate authentication credentials and issue session tokens, manage token lifecycle, enforce role-based access control for authorization decisions, maintain user session information, log all authentication and authorization events for audit compliance. Implements CON-3 and supports CRN-3. |
| Converation Orchestration Service | Manage multi-turn conversational flows and determine appropriate response strategies, maintain conversation context and history across user exchanges, coordinate between AI and NLP processing and data retrieval services, implement conversation timeouts and session cleanup, track conversation analytics and user interaction patterns, handle ambiguous queries through clarification dialogues. Central to UC-1 and UC-4. |
| Natural Language Processing Service | Analyze user queries to extract intent and entities, generate natural language responses from structured data and templates, handle ambiguous or incomplete queries with confidence scoring, manage interactions with external AI APIs or local models, implement fallback strategies for low-confidence interpretations, optimize prompts for cost and latency efficiency. Important for R5 and CRN-4. |
| Data Aggregation Service | Retrieve information from multiple university systems (LMS, registration, calendar), transform and normalize data from various sources into unified format, implement distributed caching for frequently accessed data with appropriate TTL, handle external API failures gracefully with circuit breakers, maintain connection pooling for external services, coordinate data freshness checks and cache invalidation. Supports R3, R6, and CRN-5. |
| Analytics Processing Service | Aggregate student performance data across courses and terms, calculate statistical summaries and trend analysis, generate usage reports for faculty and administrators, process historical data for predictive insights, prepare data visualizations and formatted reports, implement privacy controls for aggregated data access. Implements UC-2. |
| Event Management Service | Accept and manage event subscriptions from users based on preferences, receive system events from announcements about deadlines and grade updates, filter and route events based on user preferences and relevance, deliver events through appropriate channels, track delivery status and implement retry logic for failures, manage notification templates and formatting. Implements UC-4. |
| Data Accessing Layer | Abstract all database operations from application services, implement object-relational mapping for domain entities, enforce data integrity constraints and validation rules, manage database transactions with appropriate isolation levels, provide optimized query interfaces and prevent N+1 query problems, shield application logic from database schema details and implementation. Supports CON-6 through controlled data access. |
| External System Adapters | Encapsulate communication protocols for each external system (LMS, registration, calendar, email), implement system-specific authentication and authorization, transform external data models to internal representations, manage external API rate limits and quotas, implement circuit breakers for external system failures with automatic recovery, provide consistent error handling and logging. Critical for CRN-5 . |

### Data Storage Components

| Components | Responsibility |
| :---- | :---- |
| Primary Relational Database | Persist user accounts, roles, and preferences, store system configuration and feature flags, maintain audit logs for compliance and security, record processed analytics results and reports, ensure ACID properties for transactional data, support backup and recovery procedures. Implements CON-4 backup requirements. |
| Distributed Cache Cluster | Cache authentication tokens and user session data, store frequently accessed reference data like course catalogs and academic calendar, cache external API responses with configurable TTL, cache processed query results to reduce AI API calls, distribute load across cache nodes with data partitioning. Supports QA-1 with sub-millisecond access times. |
| Conversation History Store | Store complete conversation histories for context and analysis, maintain user interaction logs for personalization, support flexible schema for evolving conversation structures, enable efficient retrieval of recent conversation context, provide retention policy enforcement for privacy compliance. |

## **Interface Specifications**

### External Interfaces	

| Interface Name | Provider | Consumer | Description |
| :---- | :---- | :---- | :---- |
| Student Query API | API Gateway | Client Applications | Primary interface for user queries and responses. Accepts natural language queries with authentication token, user context, and conversation ID. Returns structured responses including answer text, suggested follow-ups, and conversation continuation tokens. Supports both synchronous and streaming response modes. |
| SSO Authentication | Identity Service | University Identity Provider | Validates institutional SSO tokens and establishes user sessions. Accepts SSO assertion or authorization code from institutional identity provider. Returns AIDAP session token, user profile, assigned roles, and permissions. Implements token refresh flow for session extension. |
| LMS Integration API | Data Aggregation Service | University Learning Management System | Retrieves course materials, announcements, assignments, grades, and student submission data. Implements LMS-specific authentication (API keys, OAuth). Handles LMS data models and transforms to AIDAP internal format. Includes rate limiting and pagination support. |
| Registration System API | Data Aggregation Service | University Student Information System | Accesses course catalogs, class schedules, enrollment records, academic calendar, and degree requirements. Implements registration system authentication and authorization. Provides real-time enrollment status and capacity information. Supports batch data retrieval for analytics. |
| Notification Delivery APIs | Event Management Service | Email/SMS/Push Providers | Delivers notifications through multiple channels with appropriate formatting. Email via SMTP with template rendering, SMS via provider REST APIs with character limits, push notifications via APNS/FCM. Handles delivery confirmation, bounce management, and retry logic. |

### Internal Interfaces

| Interface Name | Provider | Consumer | Description |
| :---- | :---- | :---- | :---- |
| AI Processing Interface | NLP Service | Conversation Orchestration Service | Accepts user queries with conversation context and returns structured interpretation. Input includes query text, user profile, conversation history. Output includes detected intent, extracted entities, confidence scores, suggested responses, and ambiguity flags. Supports both synchronous and asynchronous processing modes. |
| Unified Data Retrieval Interface | Data Aggregation Service | Conversation Orchestration, Analytics Services | Provides standardized access to information from all external systems, abstracting system-specific details. Supports queries for announcements, schedules, grades, course information. Returns normalized data structures with metadata (source, timestamp, freshness). Includes caching hints and error details. |
| Authentication Context Interface | Identity and Access Service | All Application Services | Provides user identity, roles, permissions, and preferences for authorization decisions. Services call this interface to validate tokens and retrieve user context. Returns user profile, role assignments, permission grants, and preference settings. Supports both token validation and direct context retrieval. |
| Event Publication Interface | Application Services | Event Management Service | Allows services to publish domain events for notification delivery. Events include type, priority, target users/groups, payload data. Uses publish-subscribe pattern for loose coupling. Supports immediate and scheduled event delivery. Provides delivery confirmation and failure tracking. |
| Cache Access Interface | Distributed Cache Cluster | All Application Services | Provides get/set operations for cached data with TTL and eviction policy management. Supports cache key namespacing, atomic operations, and batch operations. Includes cache invalidation patterns (key-based, pattern-based, tag-based). Provides cache hit/miss metrics for monitoring. |
| Data Persistence Interface | Data Access Layer | Application Services | Provides CRUD operations for domain entities with transaction management. Abstracts database implementation (SQL, document, key-value). Supports query building, pagination, sorting, filtering. Manages optimistic locking and concurrency control. Returns strongly-typed domain objects. |
| External System Adapter Interface | External System Adapters | Data Aggregation Service | Standardized interface implemented by all external system adapters. Defines common methods for data retrieval, authentication, error handling, and health checking. Enables consistent circuit breaker, retry, and fallback logic across all integrations. Supports adapter hot-swapping for testing. |
| Monitoring and Metrics Interface | Operational Services | All Services | Allows services to emit metrics, log events, and record distributed traces. Services report performance metrics (latency, throughput), business metrics (queries processed, cache hit rate), and error conditions. Supports structured logging with correlation IDs for request tracing across service boundaries. |

---

# Step 6: Sketch Views and Record Design Decisions

# ![Client Side](image1.png)![Server Side](image2.png)

![External Systems](image3.png)

### Client Side

| Layer | Element | Responsibility |
| :---- | :---- | :---- |
| Presentation | UI Modules | Render visual components, display information to users, handle layout and styling |
| Presentation | Controllers | Manage user interactions, coordinate between UI and business logic, handle navigation |
| Presentation | Chat Interface | Display conversational UI, show messages and responses, capture user text/voice input |
| Business | Session Management / Context Storage | Maintain user session state, store conversation context, manage user preferences |
| Business | Input Validation / Message Preprocessing | Validate user input before sending, format and preprocess messages, sanitize data |
| Data | Data Access Module | Handle all communication with server APIs, format requests, parse responses |
| Data | Local Cache | Store frequently accessed data locally, reduce server calls, improve performance |

### Server Side

| Layer | Element | Responsiblity |
| :---- | :---- | :---- |
| Service Interface | API Gateway | Route incoming requests, enforce rate limiting, handle API versioning |
| Service Interface | Identity & Access Service | Integrate with SSO, validate tokens, manage authentication and authorization (RBAC) |
| Service Interface | Service Endpoints | Define REST/GraphQL API contracts, handle request/response formatting |
| Application Services | Conversation Orchestration | Coordinate conversation flow, manage multi-turn dialogue, route to appropriate services |
| Application Services | Natural Language Processor | Analyze user queries, extract intent and entities, generate natural language responses |
| Application Services | Analytics Processing | Aggregate academic data, calculate statistics, generate reports for faculty |
| Application Services | Data Aggregation | Retrieve data from multiple external systems, normalize and transform data |
| Application Services | Event Management | Handle notification subscriptions, process events, route to delivery channels |
| Application Services | Operational Services | Monitor system health, collect metrics, provide logging and diagnostics |
| Business | Business Rules | Implement domain-specific rules, validate academic policies, enforce constraints |
| Business | Domain Entities | Represent core domain objects (Student, Course, Announcement, Schedule) |
| Business | Workflow Orchestration | Coordinate complex business processes, manage multi-step operations |
| Data | Data Access Layer | Abstract database operations, perform CRUD, manage transactions |
| Data | External System Adapters | Connect to LMS, Registration, Calendar, Email which handle system-specific protocols |
| Data | Distributed Cache Manager | Manage Redis cache, handle cache invalidation, optimize data retrieval |

### External Systems

| Element | Responsibility |
| :---- | :---- |
| LMS System | Provide course materials, announcements, assignments, and grades |
| Registration System | Provide course schedules, enrollment data, academic calendar |
| Calendar System | Provide academic events, deadlines, exam schedules |
| Email Server | Deliver email notifications to users |

### ![Deployment](image4.png)

| Node | Components | Responsibility |
| :---- | :---- | :---- |
| Load Balancer | Cloud Load Balancer | Distribute traffic, SSL termination, DDoS protection |
| Kubernetes Cluster | API Gateway | Route requests, rate limiting, API versioning |
| Kubernetes Cluster | Identity Service | SSO integration, token validation, RBAC |
| Kubernetes Cluster | Conversation Orchestration | Manage conversation flow and context |
| Kubernetes Cluster | NLP Service | Process natural language queries, generate responses |
| Kubernetes Cluster | Data Aggregation | Retrieve and normalize data from external systems |
| Kubernetes Cluster | Event Management | Handle notifications and event delivery |
| Data Services | PostgreSQL | Primary database for persistent data |
| Data Services | Redis | Caching for sessions and frequently accessed data |
| Data Services | Message Queue | Async event processing for notifications |
| External Systems | LMS, Registration, Calendar, Email, SSO | University systems for data and authentication |
| Client Devices | Web, Mobile, Voice | User access points |

# Step 7: Analysis of Current Design

## **Driver Analysis Table**

| Driver | Not Addressed | Partially Addressed | Completely Addressed | Design Decisions Made |
| :---- | ----- | ----- | ----- | :---- |
| UC-1: Retrieve lecture announcement |  |  | ✔ | Layered architecture establishes Conversation Orchestration, NLP Service, and Data Aggregation to support query processing and data retrieval from LMS. |
| UC-2: View Class Analytics |  |  | ✔ | Analytics Processing component aggregates data from external systems. Data Aggregation and External System Adapters enable LMS integration. |
| UC-3: System Monitoring and Maintenance |  | ✔ |  | Operational Services provides monitoring capabilities. Kubernetes supports zero-downtime deployment. CI/CD pipeline details not yet defined. |
| UC-4: Manage Notifications |  |  | ✔ | Event Management service with Message Queue enables asynchronous notification processing and multi-channel delivery. |
| QA-1: Performance  |  | ✔ |  | Distributed Cache Manager and Local Cache improve response times. Specific caching strategies and AI model optimization not yet detailed. |
| QA-2: Privacy |  | ✔ |  | Identity & Access Service provides SSO and RBAC. Detailed encryption, data masking, and audit logging not yet specified. |
| QA-3: Modifiability |  |  | ✔ | Layered architecture and modular services allow independent updates. Kubernetes enables rolling deployments. |
| QA-4: Availability/Scalability |  | ✔ |  | Kubernetes cluster with Load Balancer supports scaling. Specific auto-scaling policies and failover procedures not yet defined. |
| QA-5: Usability |  |  | ✔ | Chat Interface, UI Modules, and Controllers in Presentation Layer support intuitive conversational design. |
| CON-1: 5000 concurrent users |  | ✔ |  | Load Balancer and Kubernetes provide scaling foundation. Load testing and capacity planning not yet performed. |
| CON-2: 99.5% uptime |  | ✔ |  | Kubernetes and PostgreSQL replication support high availability. Specific SLAs and failover testing not defined. |
| CON-3: SSO authentication |  |  | ✔ | Identity & Access Service integrates with University SSO. API Gateway enforces authentication on all requests. |
| CON-4: Backup and disaster recovery |  | ✔ |  | PostgreSQL supports replication. Specific backup schedules and recovery procedures not yet defined. |
| CON-5: Cloud-native deployment |  |  | ✔ | Kubernetes-based deployment on cloud platform fully satisfies this constraint. |
| CON-6: Data retention and encryption | ✔ |  |  | No specific decisions on encryption standards, key management, or retention policies have been made. |
| CRN-1: Privacy compliance |  | ✔ |  | SSO and RBAC provide foundation. Detailed compliance measures need documentation. |
| CRN-2: Data integrity |  | ✔ |  | Data Access Layer manages transactions. Cross-system consistency needs further design. |
| CRN-3: Secure authorization |  |  | ✔ | Identity & Access Service implements RBAC. API Gateway enforces authorization. |
| CRN-4: AI response time |  | ✔ |  | Caching helps performance. AI model optimization and timeout strategies need definition. |
| CRN-5: Integration complexity |  | ✔ |  | External System Adapters isolate dependencies. Error handling and circuit breakers need detailed design. |
| CRN-6: AI cost management | ✔ |  |  | No decisions on AI model selection, usage monitoring, or cost optimization. |
