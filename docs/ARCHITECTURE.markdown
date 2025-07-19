# System Architecture

This document describes the architecture of the **Bank Enterprise Management Platform**, a microservices-based system for banking organizations. The architecture follows the **C4 Model** to provide a clear, layered view of the system.

## Context Diagram
The Context Diagram shows the system's interactions with users and external systems.

![Context Diagram](context-diagram.png)

- **Actors**: Admins, Branch Managers, Staff, and Mobile/Web App Users.
- **System**: The platform provides APIs for managing companies, branches, users, and notifications.
- **External Systems**: Core banking system, third-party email/SMS services.

## Container Diagram
The Container Diagram illustrates the main components (microservices, databases, and gateways) and their interactions.

![Container Diagram](container-diagram.png)

- **API Gateway**: Routes requests to microservices (Spring Cloud Gateway).
- **Microservices**:
  - **Auth Service**: Manages JWT-based authentication (Spring Boot).
  - **User Service**: Handles user data, roles, and groups (Spring Boot).
  - **Company Service**: Manages companies and branches (Spring Boot).
  - **Notification Service**: Sends email/SMS notifications (Spring Boot).
  - **Audit Service**: Logs activities for compliance (Spring Boot, optional).
- **Databases**: PostgreSQL (schema-per-tenant), Redis (cache/session).
- **Event Bus**: Kafka (planned) for asynchronous communication.

## Component Diagram (Auth Service)
This diagram details the internal structure of the Auth Service.

![Component Diagram](auth-component-diagram.png)

- **Controller**: Handles HTTP requests (e.g., `/login`, `/refresh-token`).
- **Service Layer**: Manages JWT generation and validation.
- **Repository**: Interacts with PostgreSQL for user credentials.

## Sequence Diagram (User Login)
The Sequence Diagram illustrates the login process.

![Sequence Diagram](login-sequence-diagram.png)

1. User sends POST `/login` to API Gateway.
2. API Gateway forwards request to Auth Service.
3. Auth Service validates credentials against PostgreSQL.
4. Auth Service stores session in Redis.
5. Auth Service returns JWT to the user.

## Design Decisions
- **Multi-Tenancy**: Schema-per-tenant in PostgreSQL for data isolation.
- **Communication**: REST/HTTP for synchronous calls, Kafka (planned) for asynchronous events.
- **Scalability**: Docker and Kubernetes for containerized deployment.
- **Security**: JWT for authentication, role-based access control.