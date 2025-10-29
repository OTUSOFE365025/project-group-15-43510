Project Overview
AIDAP is an AI-powered conversational assistant for universities. Students, faculty, and administrators can ask questions and get information about courses, schedules, deadlines, and announcements using natural language (text or voice).
Key Features: Natural language queries, multi-platform access (web/mobile/voice), integration with LMS and university systems, personalized notifications.

Deliverables
1. Use Case Models
File: Deliverable1_Requirements_Analysis.md (Section: Use Cases)
Identified 4 primary use cases:

UC-1: Student retrieves lecture announcements
UC-2: Lecturer views class analytics
UC-3: System maintainer monitors and deploys updates
UC-4: Users manage notifications

Also includes 20 detailed use cases organized by stakeholder (Students, Lecturers, Admins, Maintainers, Data Sources).
2. Quality Attributes
File: Deliverable1_Requirements_Analysis.md (Section: Quality Attributes)
Defined 10 quality attribute scenarios covering:

Performance (2 second response time)
Availability (99.5% uptime)
Security (authentication, data privacy)
Scalability (5,000 concurrent users)
Usability, Modifiability, Interoperability

Each scenario includes source, stimulus, artifact, environment, response, and measure.
3. System Constraints
File: Deliverable1_Requirements_Analysis.md (Section: System Constraints)
10 constraints identified:

Technical: Cloud deployment, SSO integration, AI models required
Business: FERPA/GDPR compliance, zero downtime updates
Project: Timeline and team limitations

4. Architectural Concerns
File: Deliverable1_Requirements_Analysis.md (Section: Architectural Concerns)
10 key concerns for ADD iterations:

System structure selection
AI model integration strategy
External system integration approach
Data synchronization design
Multi-channel support (web/mobile/voice)
Scalability, security, monitoring strategies

5. Business Case
File: Deliverable1_Requirements_Analysis.md (Section: Business Case)
Documents the problem (inefficient information access), business goals (improve student experience, reduce support burden), and success metrics (70% reduction in manual requests, 90% satisfaction).
6. Use Case Diagram
Files: AIDAP_UseCase_Diagram.png, AIDAP_UseCase_Diagram.puml
UML diagram showing 5 actors (Student, Lecturer, Administrator, System Maintainer, Data Sources) and their 20 use cases with relationships (extends, includes, triggers, uses).
7. Use Case Relationships
File: UseCase_Relationships.md
Detailed documentation of how use cases relate to each other, including relationship types, cross-stakeholder interactions, and dependency analysis.

Repository Structure
Main Documents:

README.md - This file
Deliverable1_Requirements_Analysis.md - Complete requirements analysis
UseCase_Relationships.md - Detailed use case documentation
UseCase_Diagram_Legend.md - Explanation of use case diagram
AIDAP_UseCase_Diagram.png - Visual UML diagram
AIDAP_UseCase_Diagram.puml - PlantUML source file


Next Steps
Deliverable 2 (Due Nov 16): ADD Iterations 1 & 2

Select reference architecture
Create deployment diagrams
Define major components and interfaces

Deliverable 3 (Due Dec 6): ADD Iteration 3 & ATAM Review

Complete architectural design
Implement use case
Perform ATAM scenario analysis
