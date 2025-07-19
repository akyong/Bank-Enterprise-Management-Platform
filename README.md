# Bank Enterprise Management Platform

A modular, microservices-based enterprise management system tailored for large-scale banking organizations with multiple branches and complex organizational structures. Built with **Spring Boot**, this system supports web and mobile platforms with a scalable, API-first architecture.

![Architecture Diagram](docs/architecture-diagram.png)  
*High-level architecture of the system (see `/docs/architecture`).*

## ✨ Key Features
- **Multi-Tenancy**: Schema-based isolation for managing multiple companies.
- **Branch Management**: Organize and manage branches and work units per company.
- **User Management**: Role-based and group-based access control for users.
- **Token-Based Authentication**: Secure JWT-based authentication and authorization.
- **API-First Design**: RESTful APIs for seamless integration with web and mobile apps.
- **Scalable Microservices**: Independent services for flexibility and scalability.

## 🧩 Microservices Structure
The system is divided into independent microservices, each handling a specific business domain. Each service has its own GitHub repository.

| Service Name          | Description                                      | Repository Link                     |
|-----------------------|--------------------------------------------------|------------------------------------|
| Auth Service          | Manages JWT-based authentication and authorization | [auth-service](#) |
| User Service          | Handles user data, roles, and groups             | [user-service](#) |
| Company Service       | Manages companies, branches, and work units      | [company-service](#) |
| Notification Service  | Sends email, SMS, and other notifications        | [notification-service](#) |
| Audit Service         | Logs critical activities for auditing (optional) | [audit-service](#) |
| API Gateway           | Entry point for all web and mobile requests      | [gateway-service](#) |

*Note: Replace `#` with actual repository links.*

## 🗺️ System Architecture
The system adopts a modular, loosely-coupled architecture for scalability and maintainability. Services communicate via **REST/HTTP** APIs, with plans to support **event-driven** communication using Kafka or RabbitMQ for asynchronous operations.

### Architecture Overview
- **API Gateway**: Routes requests to appropriate microservices and handles load balancing.
- **Service Layer**: Each microservice (Auth, User, Company, etc.) operates independently with its own database schema.
- **Database**: PostgreSQL with schema-based multi-tenancy; Redis for caching and session management.
- **Event Bus (Future)**: Kafka or RabbitMQ for event-driven communication (e.g., notifications, audit logs).

See [ARCHITECTURE.md](docs/ARCHITECTURE.md) for detailed diagrams, including:
- **C4 Model**: Context, Container, and Component diagrams.
- **Sequence Diagrams**: For key flows like user authentication and branch creation.

### Database Design (ERD)
The database uses **PostgreSQL** with a schema-per-tenant approach for multi-tenancy. Key entities include:
- **Company**: Stores company details (ID, name, address).
- **Branch**: Links to a company, includes branch-specific data (ID, name, location).
- **User**: Stores user details (ID, username, email, password hash).
- **Role**: Defines user roles (e.g., admin, manager, staff).
- **Group**: Groups users for access control (e.g., branch-specific groups).
- **AuditLog** (optional): Tracks critical actions for compliance.

See [DATABASE.md](docs/DATABASE.md) for the full ERD and schema details.

## 📂 Project Structure
Below is the folder structure for the main repository and microservices:

```
bank-enterprise-platform/
├── docs/                     # Documentation files
│   ├── ARCHITECTURE.md       # System architecture and diagrams
│   ├── DATABASE.md           # Database schema and ERD
│   ├── DEPLOYMENT.md         # Deployment instructions
│   ├── USER_GUIDE.md         # User guide for end-users
│   └── USECASES.md           # Use case diagrams and descriptions
├── docker/                   # Docker and Docker Compose configurations
│   ├── docker-compose.yml    # Local development setup
│   └── Dockerfile            # Base Dockerfile for microservices
├── .github/                  # GitHub Actions for CI/CD
│   └── workflows/            # CI/CD pipeline configurations
├── LICENSE                   # License file (MIT)
└── README.md                 # This file
```

Each microservice (e.g., `auth-service`) follows a similar structure:

```
auth-service/
├── src/                      # Source code
│   ├── main/                 # Main application code
│   │   ├── java/             # Spring Boot application
│   │   └── resources/        # Configuration files (application.yml)
│   └── test/                 # Unit and integration tests
├── Dockerfile                # Service-specific Dockerfile
├── pom.xml                   # Maven dependencies
└── README.md                 # Service-specific documentation
```

## 🛠️ Technology Stack
- **Backend**: Spring Boot 3
- **Database**: PostgreSQL (primary), Redis (session/cache)
- **Containerization**: Docker, Docker Compose (local), Kubernetes (production)
- **API Documentation**: OpenAPI/Swagger
- **Authentication**: JWT
- **CI/CD**: GitHub Actions

## 📚 Documentation
Comprehensive documentation is available in the `/docs` folder:
- [User Guide](docs/USER_GUIDE.md): Instructions for end-users.
- [Use Case Diagram](docs/USECASES.md): User interactions (e.g., admin creating users, managers viewing branch reports).
- [Database Design](docs/DATABASE.md): ERD and schema details.
- [Architecture Diagram](docs/ARCHITECTURE.md): C4 model and sequence diagrams.
- [Deployment Guide](docs/DEPLOYMENT.md): Local and production deployment steps.

## 🚀 Getting Started
### Prerequisites
- Java 17+
- Maven
- Docker & Docker Compose
- PostgreSQL
- Redis

### Running Locally
1. Clone the main repository:
   ```bash
   git clone https://github.com/bobby-your-username/bank-enterprise-platform.git
   ```
2. Clone each microservice repository and follow their setup instructions.
3. Initialize databases:
   ```bash
   docker-compose -f docker/docker-compose.yml up -d postgres redis
   ```
4. Run all services:
   ```bash
   docker-compose -f docker/docker-compose.yml up
   ```
5. Access the API Gateway at `http://localhost:8080`.

See [DEPLOYMENT.md](docs/DEPLOYMENT.md) for detailed instructions.

## 📖 Example API Call
Authenticate a user:
```bash
curl -X POST http://localhost:8080/auth/login \
  -H "Content-Type: application/json" \
  -d '{"username": "admin", "password": "password"}'
```

## 🤝 Contributing
We welcome contributions! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines on coding standards, pull requests, and issue reporting.

## 👨‍💻 About the Author
This project is built by **Bobby**, a passionate software engineer specializing in microservices, Spring Boot, and enterprise systems. Interested in collaborating or hiring me for your next project? Reach out!

📧 **Contact**: [bobby@example.com](mailto:bobby@example.com)  
🌐 **Portfolio**: [your-portfolio-link.com](#)  
💼 **Hire Me**: I'm available for freelance or full-time opportunities to build scalable, robust systems. DM me or check my portfolio!

## 📬 Contact
For questions or feedback, create an issue in this repository or contact [bobby@example.com].

## 📜 License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.