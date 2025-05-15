# CHAPTER 3: METHODOLOGY

## Introduction

This chapter details the methodological approach employed in developing the Letter of Recommendation (LoR) Automation System. It outlines the system architecture, design principles, implementation strategies, and the specific technologies and tools used throughout the development process. The methodology was designed to address the limitations identified in existing systems while incorporating best practices in software development and user experience design.

## Methodology

### Detailed Methodology

The development of the LoR Automation System followed a systematic approach guided by modern software engineering principles. The methodology incorporated several key phases:

#### Requirements Analysis and Planning

The project began with a comprehensive analysis of stakeholder needs and existing LoR processes. This involved:

1. **Stakeholder Interviews**: Structured interviews were conducted with alumni, faculty members, and administrative staff to understand their experiences, pain points, and expectations from an automated LoR system.

2. **Process Mapping**: The current LoR workflow was mapped in detail, from initial request to final delivery, to identify bottlenecks, redundancies, and opportunities for automation.

3. **Requirements Documentation**: Functional and non-functional requirements were documented, prioritized, and validated with stakeholders to ensure alignment with user needs.

4. **Technology Selection**: Based on the requirements analysis, appropriate technologies were selected for each system component, emphasizing scalability, security, and maintainability.

#### System Architecture Design

A microservices architecture was adopted for the LoR Automation System, decomposing the application into loosely coupled, independently deployable services. This architectural decision offers several advantages:

1. **Modularity**: Each service focuses on a specific domain function, simplifying development and maintenance.

2. **Scalability**: Services can be scaled independently based on demand, optimizing resource utilization.

3. **Technology Flexibility**: Different services can utilize different technologies as appropriate for their specific functions.

4. **Resilience**: Failures in one service do not necessarily cascade to others, enhancing system stability.

5. **Team Organization**: Development work can be distributed across teams specializing in different services.

The LoR Automation System comprises three core microservices:

1. **Authentication Service**: Manages user authentication, authorization, and token management.

2. **Alumni Service**: Handles alumni profile management, university information, and employment details.

3. **LoR Service**: Manages LoR requests, faculty assignments, draft preparation, and final delivery.

Each service is containerized using Docker and orchestrated with Docker Compose, facilitating consistent deployment across development, testing, and production environments.

#### Database Design

The system utilizes a PostgreSQL relational database, with each microservice maintaining its own database schema to ensure data independence. Key database entities include:

1. **Authentication Database**:
   - Users table (storing user credentials and roles)
   - Tokens table (managing JWT refresh tokens)

2. **Alumni Database**:
   - Alumni profiles (personal and contact information)
   - University records (educational institutions data)
   - Employment details (work history and professional information)
   - Scorecards (academic performance records)

3. **LoR Database**:
   - LoR requests (tracking all recommendation requests)
   - Faculty assignments (mapping requests to faculty members)
   - Draft and final documents (storing recommendation content)

The database design follows normalization principles to minimize redundancy while ensuring data integrity through appropriate relationships and constraints.

#### API Design and Implementation

RESTful APIs were designed to facilitate communication between frontend clients and backend services, as well as between microservices. The API design followed these principles:

1. **Resource-Oriented Design**: APIs are structured around resources (e.g., alumni, requests) rather than operations.

2. **Standard HTTP Methods**: CRUD operations are mapped to standard HTTP methods (GET, POST, PUT, DELETE).

3. **Consistent Response Format**: API responses follow a uniform structure, including status codes, messages, and data payloads.

4. **Versioning**: API endpoints include version indicators to support backward compatibility during updates.

5. **Documentation**: All APIs are documented using Swagger/OpenAPI, providing interactive documentation for developers.

Implementation of these APIs leveraged Spring Boot's robust web framework, which offers built-in support for RESTful service development, validation, and exception handling.

#### Frontend Development

The frontend of the LoR Automation System was developed using React.js, a popular JavaScript library for building user interfaces. The frontend development followed these principles:

1. **Component-Based Architecture**: The UI is decomposed into reusable components that encapsulate specific functionality and appearance.

2. **Responsive Design**: The interface adapts to different screen sizes and devices, ensuring accessibility across platforms.

3. **State Management**: Application state is managed using React's Context API and custom hooks, maintaining a predictable state flow.

4. **Role-Based Views**: Different user interfaces are presented based on user roles (alumni, faculty, administrator), showing only relevant functionality.

5. **Asynchronous Communication**: The frontend communicates with backend services asynchronously, providing feedback to users during operations.

The frontend development utilized additional libraries such as Axios for API communication, TailwindCSS for styling, and React Router for navigation management.

#### Security Implementation

Security was prioritized throughout the development process, with implementation of:

1. **JWT-Based Authentication**: JSON Web Tokens are used for secure authentication, with tokens validated at the API gateway and individual service levels.

2. **Role-Based Access Control**: Different user roles (alumni, faculty, administrator) have distinct permissions, enforced at both frontend and backend levels.

3. **Input Validation**: All user inputs are validated on both client and server sides to prevent injection attacks.

4. **Cross-Origin Resource Sharing (CORS)**: CORS policies are configured to control which domains can access the APIs.

5. **Secure Password Handling**: User passwords are hashed using bcrypt before storage, and password complexity requirements are enforced.

6. **HTTPS Communication**: All API communication occurs over HTTPS to ensure data confidentiality in transit.

#### Testing Strategy

A comprehensive testing strategy was implemented to ensure system quality:

1. **Unit Testing**: Individual components and functions are tested in isolation using JUnit for backend services and Jest for frontend components.

2. **Integration Testing**: Interactions between components and services are tested to verify correct behavior when integrated.

3. **API Testing**: RESTful endpoints are tested using tools like Postman and automated test scripts to verify correct functionality.

4. **User Interface Testing**: Frontend components are tested for proper rendering, event handling, and state management.

5. **Load Testing**: The system is tested under various load conditions to ensure performance under expected usage patterns.

6. **Security Testing**: Vulnerability assessments and penetration testing are conducted to identify and address security weaknesses.

#### Deployment and DevOps

The deployment process leverages containerization and orchestration:

1. **Containerization**: Each microservice is packaged as a Docker container, ensuring consistency across environments.

2. **Orchestration**: Docker Compose manages the deployment and interaction of containers, simplifying the deployment process.

3. **Environment Configuration**: Environment-specific configurations are managed using Docker environment variables, facilitating deployment across development, testing, and production environments.

4. **Logging and Monitoring**: Centralized logging and monitoring are implemented to track system performance and identify issues.

### Assumptions Made

During the design and implementation of the LoR Automation System, several assumptions were made:

1. **User Authentication**: The system assumes that users can be uniquely identified by their email addresses and that they have access to those email addresses for verification purposes.

2. **Faculty Availability**: It is assumed that faculty members have access to the system and will respond to LoR requests within a reasonable timeframe.

3. **Data Accessibility**: The system assumes that basic alumni academic records are available for integration or can be provided by alumni during registration.

4. **Internet Connectivity**: Users are expected to have reliable internet access to interact with the web-based system.

5. **Browser Compatibility**: The system is designed for modern web browsers (Chrome, Firefox, Safari, Edge) and may not function optimally on older browsers.

6. **Concurrent User Load**: The system is designed to handle up to 500 concurrent users without significant performance degradation.

7. **Database Integrity**: It is assumed that the database will maintain referential integrity and that appropriate backup mechanisms are in place.

### Design & Modelling

#### System Architecture Diagram

The LoR Automation System follows a microservices architecture pattern, with three primary services interacting through RESTful APIs. The high-level architecture is illustrated below:

```
                          +--------------+
                          |              |
                          |  React.js    |
                          |  Frontend    |
                          |              |
                          +--------------+
                                 |
                                 | HTTP/HTTPS
                                 |
                          +--------------+
                          |              |
                          |   API        |
                          |   Gateway    |
                          |              |
                          +--------------+
                                 |
                 +---------------+---------------+
                 |               |               |
        +----------------+ +-------------+ +-------------+
        |                | |             | |             |
        | Authentication | |   Alumni    | |    LoR      |
        |    Service     | |   Service   | |   Service   |
        |                | |             | |             |
        +----------------+ +-------------+ +-------------+
                |               |               |
        +----------------+ +-------------+ +-------------+
        |                | |             | |             |
        | Authentication | |   Alumni    | |    LoR      |
        |    Database    | |   Database  | |   Database  |
        |                | |             | |             |
        +----------------+ +-------------+ +-------------+
```

#### Entity Relationship Diagram

The database design follows a normalized approach, with clear relationships between entities. The simplified ER diagram below illustrates the key entities and their relationships:

**Authentication Database**:
```
User (id, username, password, email, role, created_at, updated_at)
Token (id, user_id, refresh_token, expiry_date, created_at)
```

**Alumni Database**:
```
Alumni (registration_id, first_name, last_name, date_of_birth, learner_mail_address, personal_mail, mobile_number, status)
University (id, name, location, country, website)
EmploymentDetail (id, registration_id, company_name, position, start_date, end_date, is_current)
Scorecard (id, registration_id, semester, gpa, year, document_url)
```

**LoR Database**:
```
LorRequest (request_id, registration_id, faculty_id, status, draft_lor, rejection_remarks, final_lor, request_date)
```

#### Sequence Diagrams

The following sequence diagram illustrates the typical flow of a LoR request process:

```
Alumni                      System                       Faculty                      Admin
  |                            |                            |                            |
  | Submit LoR Request         |                            |                            |
  |--------------------------->|                            |                            |
  |                            | Create Request             |                            |
  |                            |--------------------------->|                            |
  |                            |                            |                            |
  | Request Confirmation       |                            |                            |
  |<---------------------------|                            |                            |
  |                            |                            |                            |
  |                            | Notification               |                            |
  |                            |--------------------------->|                            |
  |                            |                            |                            |
  |                            |                            | Review Request             |
  |                            |                            |------------------------    |
  |                            |                            |                       |    |
  |                            |                            |<-----------------------    |
  |                            |                            |                            |
  |                            |                            | Submit Decision            |
  |                            |<---------------------------|                            |
  |                            |                            |                            |
  |                            | Process Decision           |                            |
  |                            |------------------------------------------------>|      |
  |                            |                            |                     |      |
  |                            |<------------------------------------------------|      |
  |                            |                            |                            |
  | Notification               |                            |                            |
  |<---------------------------|                            |                            |
  |                            |                            |                            |
```

#### Component Diagrams

The React frontend is organized into several key components, as illustrated in the component diagram below:

```
                      +----------------+
                      |                |
                      |    App.jsx     |
                      |                |
                      +----------------+
                             |
         +------------------+|+------------------+
         |                   |                   |
+----------------+ +----------------+ +----------------+
|                | |                | |                |
| LoginPage.jsx  | |AdminDashboard | |AlumniDashboard |
|                | |                | |                |
+----------------+ +----------------+ +----------------+
                                       |
                     +----------------+|+------------------+
                     |                 |                   |
            +----------------+ +----------------+ +----------------+
            |                | |                | |                |
            |SubmitLorRequest| |EmploymentDetail| |UploadScorecard |
            |                | |                | |                |
            +----------------+ +----------------+ +----------------+
```

### Module Specifications

#### Authentication Service

The Authentication Service manages user identity, authentication, and authorization. Key features include:

1. **User Registration**: Creates new user accounts with appropriate roles.
2. **Login/Logout**: Handles user session management through JWT tokens.
3. **Password Management**: Supports secure password reset and recovery.
4. **Role Management**: Assigns and verifies user roles and permissions.
5. **Token Validation**: Verifies the authenticity of JWT tokens for secure API access.

#### Alumni Service

The Alumni Service manages alumni profiles and related information. Key features include:

1. **Profile Management**: Enables alumni to create and update their profiles.
2. **University Management**: Maintains a database of educational institutions.
3. **Employment History**: Tracks alumni professional experience.
4. **Academic Records**: Stores and validates academic performance data.
5. **Alumni Search**: Provides secure search functionality for administrators and faculty.

#### LoR Service

The LoR Service manages the recommendation request workflow. Key features include:

1. **Request Submission**: Allows alumni to submit LoR requests to specific faculty.
2. **Request Tracking**: Provides status updates on pending requests.
3. **Faculty Interface**: Enables faculty to view, accept, reject, and complete LoR requests.
4. **Draft Management**: Supports the creation and revision of recommendation letters.
5. **Delivery Management**: Facilitates secure delivery of completed recommendations.

#### Frontend Components

The React frontend consists of several key components:

1. **Authentication Components**: Login, registration, and password recovery interfaces.
2. **Alumni Dashboard**: Personalized interface for alumni to manage profiles and requests.
3. **Faculty Dashboard**: Interface for faculty to manage and respond to LoR requests.
4. **Admin Dashboard**: Administrative interface for system oversight and management.
5. **Shared Components**: Reusable UI elements like navigation bars, forms, and modals.

### Justification for Modules

#### Microservices Architecture

The decision to adopt a microservices architecture was based on several key considerations:

1. **Scalability**: Individual services can be scaled independently based on demand, optimizing resource utilization.
2. **Maintainability**: Smaller, focused services are easier to understand, develop, and maintain.
3. **Resilience**: Failures in one service don't necessarily affect others, improving system robustness.
4. **Deployment Flexibility**: Services can be updated individually without requiring system-wide deployments.
5. **Team Organization**: Development work can be distributed across teams specializing in different services.

#### Separation of Authentication

Authentication is implemented as a separate service for several reasons:

1. **Security Isolation**: Separating authentication logic reduces the attack surface for security vulnerabilities.
2. **Reusability**: A dedicated authentication service can be reused across multiple applications.
3. **Specialized Expertise**: Security-critical code can be developed and reviewed by specialists.
4. **Compliance**: Isolation simplifies compliance with security standards and regulations.

#### Alumni Service Independence

The Alumni Service is separated from the LoR Service for these reasons:

1. **Data Management**: Alumni data has distinct management requirements from LoR data.
2. **Functional Cohesion**: The service focuses on alumni profile management, a cohesive set of functions.
3. **Potential Reuse**: Alumni information may be useful for other institutional applications beyond LoRs.
4. **Data Sensitivity**: Different security and privacy requirements apply to personal vs. recommendation data.

#### Frontend Component Structure

The React component structure follows best practices for several reasons:

1. **Reusability**: Components encapsulate specific functionality and can be reused across the application.
2. **Maintainability**: Smaller, focused components are easier to understand and modify.
3. **Testing**: Isolated components can be tested independently, improving test coverage.
4. **Performance**: Component-based architecture facilitates optimization through techniques like memoization.
5. **Collaboration**: Different team members can work on different components simultaneously.

## Tools Used

### Backend Development

1. **Java 17**: The primary programming language for backend services, chosen for its robustness, performance, and strong typing.

2. **Spring Boot 3.0**: A framework that simplifies the development of Java applications, providing auto-configuration, dependency injection, and embedded servers.

3. **Spring Security**: Handles authentication, authorization, and other security features, integrated with JWT for stateless authentication.

4. **Spring Data JPA**: Simplifies database operations through repository abstractions, reducing boilerplate code.

5. **Hibernate**: An Object-Relational Mapping (ORM) framework that facilitates mapping between Java objects and database tables.

6. **PostgreSQL 14**: A powerful, open-source relational database management system known for its reliability and feature set.

7. **Lombok**: A Java library that reduces boilerplate code for model/data objects through annotations.

8. **MapStruct**: A code generator that simplifies the implementation of mappings between Java bean types.

9. **Swagger/OpenAPI**: Tools for API documentation and exploration, making it easier for developers to understand and use the APIs.

### Frontend Development

1. **React.js 18**: A JavaScript library for building user interfaces, chosen for its component-based architecture and virtual DOM performance.

2. **TailwindCSS**: A utility-first CSS framework that facilitates rapid UI development with consistent styling.

3. **Axios**: A promise-based HTTP client for making API requests from the browser.

4. **React Router**: A standard library for routing in React applications, enabling navigation between different components.

5. **React Icons**: A collection of popular icons for React applications, providing visual elements for the UI.

6. **Zustand**: A small, fast state-management solution for React applications, used for global state management.

### DevOps and Deployment

1. **Docker**: A platform for developing, shipping, and running applications in containers, ensuring consistency across environments.

2. **Docker Compose**: A tool for defining and running multi-container Docker applications, simplifying the orchestration of microservices.

3. **Git**: A distributed version control system for tracking changes in source code during development.

4. **GitHub**: A platform for hosting and collaborating on Git repositories, facilitating team collaboration.

5. **Maven**: A build automation tool used primarily for Java projects, managing dependencies and the build lifecycle.

### Testing Tools

1. **JUnit 5**: A framework for writing and running tests in Java, used for unit testing backend services.

2. **Mockito**: A mocking framework for unit tests in Java, allowing the creation of test doubles for dependencies.

3. **Jest**: A JavaScript testing framework optimized for React applications, used for testing frontend components.

4. **React Testing Library**: A set of utilities that encourage good testing practices for React components.

5. **Postman**: A platform for API development and testing, used for manual and automated API testing.

### Code Quality and Documentation

1. **SonarQube**: A static code analysis tool that detects bugs, vulnerabilities, and code smells in the codebase.

2. **ESLint**: A static code analysis tool for identifying problematic patterns in JavaScript code.

3. **Prettier**: A code formatter that ensures consistent code style across the frontend codebase.

4. **JavaDoc**: A documentation generator for Java that produces HTML documentation from Java source code.

5. **Markdown**: A lightweight markup language used for documentation, including README files and project notes.

## Preliminary Result Analysis

During the development process, several preliminary tests were conducted to validate the approach and identify potential issues:

### Performance Testing

Initial load testing with simulated users indicated that the system could handle approximately 200 concurrent users with response times under 500ms for most operations. The microservices architecture demonstrated effective resource utilization, with CPU usage distributed appropriately across services.

### Security Assessment

Preliminary security testing identified and addressed several potential vulnerabilities:

1. **CORS Misconfiguration**: Initial CORS settings were too permissive and were adjusted to restrict access to authorized domains.

2. **Token Expiration**: JWT token expiration was optimized to balance security and user experience, with refresh token mechanisms implemented.

3. **Input Validation**: Additional validation was added for user inputs to prevent injection attacks and data corruption.

### Usability Testing

Early usability testing with a small group of users (5 alumni, 3 faculty members) provided valuable feedback:

1. **Navigation Complexity**: Initial feedback indicated that the navigation structure was confusing for some users, leading to a redesign of the main navigation components.

2. **Form Clarity**: Users requested more guidance during form completion, resulting in the addition of inline help text and validation feedback.

3. **Status Visibility**: Alumni expressed a desire for clearer status indicators for their LoR requests, prompting the development of an enhanced status tracking component.

These preliminary findings informed refinements to the system design and implementation before final deployment.

## Conclusions

The methodology adopted for the LoR Automation System emphasizes modern software engineering practices, including:

1. **Microservices Architecture**: Decomposing the system into independent, specialized services enhances maintainability, scalability, and resilience.

2. **User-Centered Design**: Prioritizing user needs through stakeholder interviews, usability testing, and iterative refinement ensures a system that effectively serves its intended audience.

3. **Security by Design**: Incorporating security considerations from the earliest stages of development helps protect sensitive academic and personal information.

4. **DevOps Approach**: Leveraging containerization and automation streamlines deployment and maintenance processes.

5. **Comprehensive Testing**: Multi-level testing strategies ensure system quality and reliability.

The detailed methodology described in this chapter lays the foundation for the implementation and results discussed in subsequent chapters. The choices made in architecture, design, and technology selection directly address the limitations identified in existing systems while incorporating best practices from industry and academia.
