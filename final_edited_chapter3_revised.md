# CHAPTER 3: METHODOLOGY

## Introduction

In this chapter, I'll detail the methodological approach used to develop our Letter of Recommendation (LoR) Generation System. I'll present the actual system architecture, design principles, implementation strategies, and specific technologies chosen throughout the development process. Our methodology directly addresses the limitations identified in existing systems while incorporating best practices in software development and user experience design.

## Methodology

### Development Approach

We followed a systematic approach guided by modern software engineering principles, implementing the system over a 4-month period from January to May 2025. The development was organized into distinct phases with specific objectives for each:

#### Requirements Analysis and Planning (Weeks 1-3)

We began by understanding the requirements and planning the overall system architecture:

1. **Project Definition**: We finalized the project topic and defined key requirements for the LoR Generation System. This included identifying the primary stakeholders (alumni, faculty, and administrators) and their specific needs.

2. **Technology Research**: We researched and learned the basics of Spring Boot for backend development and Docker for containerization and deployment. This initial learning phase was crucial for making informed architectural decisions.

3. **Database Design**: We discussed and finalized the structure of the database tables, focusing particularly on the fields necessary for alumni verification and LoR requests. This included planning the relationships between entities and defining primary/foreign key relationships.

4. **System Planning**: We mapped out the overall website layout and defined the frontend and backend flow for data retrieval and submission. This planning phase helped establish a clear vision for the user journey and system interactions.

#### Initial System Setup (Weeks 4-5)

With requirements and planning in place, we proceeded to set up the basic system components:

1. **Backend Foundation**: We established a Spring Boot backend with PostgreSQL and Spring Data JPA. This included configuring the development environment, setting up database connections, and implementing basic project structure.

2. **Data Model Implementation**: We created the initial database tables to store student details, focusing on the core information needed for verification and identification.

3. **API Development**: We developed the first API endpoint to verify student details using registration number, email, and date of birth. This formed the foundation for user authentication in the system.

4. **Frontend Initialization**: We developed the first page using React and Tailwind CSS, creating input fields for registration number, email, and date of birth. This established the entry point for alumni accessing the system.

5. **API Integration**: We configured Axios to send requests from the frontend to the backend, establishing the communication pattern that would be used throughout the application.

#### LoR Request Module Development (Weeks 5-8)

The next phase focused on developing the core functionality for managing LoR requests:

1. **Entity Development**: We created the LoRRequest entity, DTO (Data Transfer Object), repository, service, and controller components. This established the complete stack for handling LoR requests from database to API.

2. **Unique Identification**: We implemented a unique LoR ID generation system in a specified format to ensure each request could be distinctly tracked and referenced.

3. **Frontend Integration**: We designed and integrated a frontend submission page with the backend API, allowing alumni to submit their LoR requests through an intuitive interface.

4. **Validation Implementation**: We defined and implemented schema validation for incoming LoR requests to ensure data integrity and prevent invalid submissions.

5. **Notification System**: We developed an EmailService to send confirmation and status update emails to alumni, enhancing communication throughout the LoR process.

6. **Document Management**: We implemented a structured approach for document submissions, including a folder organization system (YYYY/MM/DD/) and database schema for storing document metadata.

7. **Alumni Service**: We developed an AlumniService with search functionality, update capabilities, validation rules, and error handling to ensure robust request processing.

8. **Pagination**: We implemented fetching LoR requests with pagination, ensuring the response includes total count, per_page, current_page, and total_pages for efficient data retrieval.

#### Document Management System (Weeks 9-10)

This phase focused on enhancing the document handling capabilities:

1. **File Storage Structure**: We implemented a robust file storage structure for LoR documents, organizing files in a logical hierarchy for easy retrieval and management.

2. **Upload API**: We developed both single and multiple file upload APIs, allowing users to submit necessary documentation with their LoR requests.

3. **Validation Rules**: We added comprehensive file validation, including limits on the number of files (maximum 5) and file size (5MB each) to ensure system performance and security.

4. **Metadata Management**: We created a system for storing document metadata in the database, linking uploaded files to their respective LoR requests and maintaining important information about each document.

5. **Retrieval Endpoints**: We implemented document retrieval endpoints, allowing authorized users to access previously uploaded documents when needed.

#### Authentication and Faculty Interface (Weeks 11-13)

Security and faculty functionality were the focus of this development phase:

1. **JWT Authentication**: We implemented JWT-based authentication to secure the application, replacing basic authentication with a more robust token-based approach.

2. **Access Control**: We added role-based access control to ensure different user types (alumni, faculty, administrators) could only access appropriate functionality.

3. **Faculty Dashboard**: We developed wireframes and implementation for the faculty dashboard, providing a dedicated interface for reviewing and processing LoR requests.

4. **Review Interface**: We created a faculty request review interface that presents all necessary information for evaluating LoR requests and making decisions.

5. **Token Validation**: We implemented secure token validation in API requests to maintain security throughout the application.

6. **Status Updates**: We added endpoints for updating request status, allowing faculty to approve, reject, or request modifications to LoR requests.

#### LoR Generation and Notifications (Weeks 14-15)

This phase focused on the core LoR generation functionality:

1. **ML Integration**: We developed integration with a machine learning model for draft LoR generation, automating the initial creation of recommendation letters based on student data.

2. **Template Management**: We created a system for managing LoR templates, providing standardized formats while allowing for customization.

3. **Draft Editing**: We implemented an interface for faculty to edit draft recommendations before finalization, ensuring the quality and accuracy of generated letters.

4. **PDF Generation**: We added functionality to generate PDF versions of final LoRs, creating professional documents ready for submission.

5. **Status Notifications**: We created a notification system to alert users about status updates, ensuring all stakeholders remained informed throughout the process.

#### System Completion and Documentation (Weeks 16-18)

The final phase focused on completing the system and ensuring comprehensive documentation:

1. **API Refinement**: We added the GET /alumni-detail/{id} endpoint to retrieve alumni details and integrated a standardized response structure with proper error handling.

2. **Scorecard Management**: We designed and implemented Scorecard APIs for managing academic performance records, enhancing the information available for LoR generation.

3. **API Documentation**: We added Swagger (OpenAPI) documentation for all backend endpoints, tagging and describing each API for easier integration and testing.

4. **Containerization**: We dockerized the backend services using a docker-compose.yml file that includes PostgreSQL, alumni-service, and lor-service, ensuring proper communication between services and adding a persistent volume to retain PostgreSQL data.

5. **Frontend Completion**: We completed the frontend setup for the LoR system using React and Tailwind CSS, configuring routes for login, alumni search, update, and dashboard.

6. **Responsive Design**: We built responsive search, update, and dashboard UI components to ensure the system worked effectively across different devices and screen sizes.

### System Architecture

Our LoR Generation System follows a modern, layered architecture pattern:

#### Backend Architecture

The backend is built using Spring Boot with a layered approach:

1. **Controller Layer**: Handles HTTP requests and responses, implementing REST endpoints for client communication. Controllers are organized by domain (authentication, alumni, LoR) and use DTOs for data transfer.

2. **Service Layer**: Contains business logic and orchestrates operations across multiple repositories. Services implement transaction management and ensure business rules are enforced.

3. **Repository Layer**: Provides data access using Spring Data JPA, with repositories defined for each entity to handle database operations.

4. **Entity Layer**: Defines the data model using JPA annotations, mapping Java objects to database tables with appropriate relationships.

5. **DTO Layer**: Provides data transfer objects that define the structure of data exchanged between the frontend and backend, ensuring clean separation of concerns.

6. **Exception Handling**: Implements a global error handler using Spring's @ControllerAdvice to provide consistent error responses across all endpoints.

#### Frontend Architecture

The frontend is developed using React.js with a component-based approach:

1. **Component Structure**: UI elements are organized into reusable components, enhancing maintainability and consistency.

2. **Routing**: React Router manages navigation between different views, providing a seamless single-page application experience.

3. **API Integration**: Axios handles communication with backend services, with dedicated API modules for different domains.

4. **Responsive Design**: Tailwind CSS provides utility-first styling that ensures the application works well across different devices and screen sizes.

5. **Form Management**: Forms for data entry are implemented with validation to ensure data integrity before submission to the backend.

### Database Design

We chose PostgreSQL for our relational database, with a normalized schema design:

#### Key Entities

1. **Users**: Stores authentication information including credentials and roles.

2. **Alumni**: Contains alumni personal information, contact details, and relationships to academic records.

3. **LoRRequests**: Tracks all recommendation requests, including status, timestamps, and relationships to alumni and faculty.

4. **Scorecards**: Stores academic performance records that can be referenced during LoR generation.

5. **Documents**: Manages metadata for uploaded files, including paths, types, and relationships to requests.

6. **Universities**: Contains information about universities for which LoRs are requested.

#### Entity Relationships

1. **Alumni to LoRRequests**: One-to-many relationship, as an alumnus can submit multiple LoR requests.

2. **LoRRequests to Documents**: One-to-many relationship, as each request can have multiple supporting documents.

3. **Alumni to Scorecards**: One-to-many relationship, as an alumnus has multiple academic records.

4. **Users to Alumni**: One-to-one relationship, linking authentication information to alumni profiles.

### API Design

Our API follows REST principles with a focus on consistency and usability:

1. **Resource-Oriented Design**: APIs are structured around resources (alumni, requests, documents) rather than operations.

2. **Standard HTTP Methods**: We map CRUD operations to standard HTTP methods (GET, POST, PUT, DELETE).

3. **Consistent Response Format**: All API responses follow a uniform structure using ApiResponseDto for success and ErrorResponseDto for errors.

4. **Pagination Support**: List endpoints implement pagination with consistent parameters and response structure.

5. **Comprehensive Documentation**: Swagger annotations document all endpoints, making the API self-describing and easier to use.

### Security Implementation

Security was a primary concern throughout development:

1. **JWT Authentication**: Token-based authentication using JSON Web Tokens with secure storage and validation.

2. **Role-Based Access Control**: Different user roles (alumni, faculty, admin) have appropriate permissions.

3. **Input Validation**: Comprehensive validation on both client and server sides prevents injection attacks and data corruption.

4. **Secure File Handling**: Validation of file types, sizes, and content to prevent security vulnerabilities.

5. **Error Handling**: The global error handler ensures sensitive information is not exposed in error responses.

### Challenges and Solutions

During the implementation, we encountered several challenges and developed effective solutions:

1. **Challenge**: Ensuring proper validation of input data, especially for date fields, to maintain consistency across the system.
   **Solution**: Implemented comprehensive validation at both frontend and backend, with standardized date formats and clear error messages.

2. **Challenge**: Handling file uploads efficiently while keeping the storage structured and accessible.
   **Solution**: Developed a hierarchical storage structure (YYYY/MM/DD/) with metadata tracking in the database.

3. **Challenge**: Implementing pagination correctly while maintaining performance.
   **Solution**: Used Spring Data's pagination support with optimized queries and index creation.

4. **Challenge**: Integrating the frontend with the backend in a standardized way.
   **Solution**: Created consistent API response formats and centralized API client code.

5. **Challenge**: Debugging and refining error handling mechanisms to provide meaningful responses.
   **Solution**: Implemented a global error handler that provides consistent, informative error responses.

### Development Tools and Environment

The development environment was configured to support efficient development:

1. **Version Control**: Git for source code management and collaboration.

2. **IDE**: IntelliJ IDEA for backend development and Visual Studio Code for frontend development.

3. **Containerization**: Docker and Docker Compose for consistent development and deployment environments.

4. **API Testing**: Postman for manual API testing and documentation.

5. **Database Management**: pgAdmin for PostgreSQL database administration.

## Conclusion

The methodology described in this chapter reflects the actual implementation approach for our LoR Generation System. By following a structured development process with clear phases and objectives, we successfully built a comprehensive system that addresses the needs of all stakeholders. The architecture decisions, technology choices, and implementation strategies were guided by best practices in software engineering and informed by the specific requirements of the LoR generation process.

The detailed timeline and phase-based approach allowed us to manage complexity and deliver a complete solution within the 4-month project timeframe. Each phase built upon the previous one, gradually expanding the system's capabilities while maintaining a focus on quality, security, and user experience.

In the next chapter, we will analyze the results of our implementation, evaluating how well the system meets its objectives and the impact it has on the LoR process.
