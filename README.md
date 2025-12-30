# Conference Management System

A comprehensive microservices-based conference management platform built with Spring Boot and Angular. This system provides a scalable and maintainable solution for organizing and managing academic and professional conferences.

![Java](https://img.shields.io/badge/Java-62.8%25-orange)
![TypeScript](https://img.shields.io/badge/TypeScript-27.4%25-blue)
![HTML](https://img.shields.io/badge/HTML-9.6%25-red)
![CSS](https://img.shields.io/badge/CSS-0.2%25-purple)

## Table of Contents

- [Overview](#overview)
- [System Architecture](#system-architecture)
- [Microservices](#microservices)
- [Technology Stack](#technology-stack)
- [Getting Started](#getting-started)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
- [License](#license)

## Overview

The Conference Management System is designed to streamline the entire conference lifecycle, from initial planning and registration to keynote management and event coordination. Built on a microservices architecture, the system ensures high availability, scalability, and maintainability.

### Key Features

- **Conference Management**: Create, update, and manage multiple conferences
- **Keynote Speaker Management**: Organize and schedule keynote sessions
- **Service Discovery**: Automatic service registration and discovery
- **Centralized Configuration**: Dynamic configuration management across all services
- **API Gateway**: Single entry point for all client requests with intelligent routing
- **Responsive Frontend**: Modern Angular-based user interface

## System Architecture

This application follows a microservices architecture pattern with the following components:

```
┌─────────────────────────────────────────────────────────────┐
│                    Angular Frontend                          │
│              (management-app-angular)                        │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                   API Gateway Service                        │
│              (gateway-service:8888)                          │
└──────────┬──────────────────────────────────────┬───────────┘
           │                                       │
           ▼                                       ▼
┌──────────────────────┐              ┌──────────────────────┐
│  Discovery Service   │◄─────────────┤  Config Service      │
│   (Eureka:8761)     │              │   (Spring Cloud)     │
└──────────┬───────────┘              └──────────────────────┘
           │
           │ Service Registration
           │
    ┌──────┴──────┬──────────────┐
    ▼             ▼              ▼
┌─────────┐  ┌─────────┐  ┌─────────┐
│Conference│  │ Keynote │  │  Other  │
│ Service │  │ Service │  │Services │
└─────────┘  └─────────┘  └─────────┘
```

## Microservices

### 1. Discovery Service (Eureka Server)

**Port**: 8761  
**Purpose**: Service registry and discovery

The Discovery Service acts as the central registry for all microservices in the system. It enables service-to-service communication without hardcoded URLs.

**Key Responsibilities**:
- Service registration: All microservices register themselves on startup
- Service discovery: Services can locate each other dynamically
- Health monitoring: Tracks the health status of all registered services
- Load balancing: Provides client-side load balancing information

**Technology**: Netflix Eureka

### 2. Config Service (Spring Cloud Config Server)

**Purpose**: Centralized configuration management

The Config Service provides centralized external configuration for all microservices, supporting different environments (development, staging, production).

**Key Responsibilities**:
- Centralized configuration: Single source of truth for all application properties
- Environment-specific configurations: Separate configs for dev, test, and production
- Dynamic configuration updates: Services can refresh configurations without restart
- Version control integration: Can pull configurations from Git repositories
- Security: Encrypted property values for sensitive data

**Benefits**:
- Eliminates configuration duplication across services
- Enables configuration changes without redeployment
- Supports configuration versioning and audit trails

### 3. Gateway Service (API Gateway)

**Port**: 8888  
**Purpose**: Single entry point and request routing

The Gateway Service serves as the front door to all microservices, providing a unified API interface and handling cross-cutting concerns.

**Key Responsibilities**:
- Request routing: Directs incoming requests to appropriate microservices
- Load balancing: Distributes requests across multiple service instances
- Authentication & Authorization: Validates user credentials and permissions
- Rate limiting: Prevents service overload with request throttling
- Request/Response transformation: Modifies requests and responses as needed
- Circuit breaking: Provides fallback mechanisms for failed services
- Monitoring and logging: Centralized logging of all API requests

**Technology**: Spring Cloud Gateway

**Advantages**:
- Simplifies client-side code by providing a single endpoint
- Reduces the number of round trips
- Implements security at the edge
- Enables easier API versioning

### 4. Conference Service

**Purpose**: Core conference management functionality

The Conference Service handles all operations related to conference management, including creation, updates, and organization.

**Key Responsibilities**:
- Conference CRUD operations: Create, read, update, and delete conferences
- Conference metadata management: Dates, venues, themes, descriptions
- Registration management: Track attendee registrations
- Session scheduling: Organize conference sessions and tracks
- Abstract/Paper submission: Handle paper submissions and reviews
- Participant management: Manage speakers, attendees, and organizers

**Key Features**:
- RESTful API endpoints for conference operations
- Database integration for persistent storage
- Business logic for conference workflows
- Integration with other services via service discovery

### 5. Keynote Service

**Purpose**: Keynote speaker and session management

The Keynote Service specializes in managing keynote speakers and their sessions within conferences.

**Key Responsibilities**:
- Keynote speaker management: Store speaker profiles, bios, and contact information
- Session scheduling: Schedule and manage keynote presentations
- Speaker assignments: Assign speakers to specific time slots and venues
- Keynote content management: Store presentation materials and abstracts
- Speaker communication: Integration points for speaker notifications

**Key Features**:
- Speaker profile management
- Session time slot management
- Conflict detection for scheduling
- Speaker availability tracking

### 6. Management App (Angular Frontend)

**Technology**: Angular  
**Purpose**: User interface

The frontend application provides an intuitive, responsive interface for all user interactions with the system.

**Key Features**:
- Modern, responsive UI design
- Conference dashboard for organizers
- Registration interfaces for attendees
- Admin panel for system management
- Real-time updates and notifications
- Multi-role support (admin, organizer, attendee, speaker)

**Capabilities**:
- Conference browsing and search
- User registration and authentication
- Conference creation and management (organizers)
- Keynote session viewing and management
- Responsive design for mobile and desktop

## Technology Stack

### Backend
- **Framework**: Spring Boot 3.x
- **Language**: Java 17+
- **Service Discovery**: Netflix Eureka
- **API Gateway**: Spring Cloud Gateway
- **Configuration**: Spring Cloud Config
- **Database**: MySQL/PostgreSQL
- **Build Tool**: Maven
- **Communication**: RESTful APIs, OpenFeign

### Frontend
- **Framework**: Angular 15+
- **Language**: TypeScript
- **Styling**: CSS3, Bootstrap/Material Design
- **Build Tool**: Angular CLI

### DevOps & Tools
- **Version Control**: Git
- **Containerization**: Docker (recommended)
- **API Testing**: Postman
- **IDE**: IntelliJ IDEA / VS Code

## Getting Started

### Prerequisites

Before running the application, ensure you have the following installed:

- **Java Development Kit (JDK)**: Version 17 or higher
- **Maven**: Version 3.8 or higher
- **Node.js**: Version 16 or higher
- **npm**: Version 8 or higher
- **MySQL/PostgreSQL**: Latest stable version
- **Git**: For cloning the repository

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/ayoubouhensous/Conference_Management_System.git
   cd Conference_Management_System
   ```

2. **Set up the databases**
   
   Create separate databases for each service:
   ```sql
   CREATE DATABASE conference_db;
   CREATE DATABASE keynote_db;
   ```

3. **Configure database connections**
   
   Update the `application.properties` or `application.yml` files in each service with your database credentials.

## Configuration

### Config Service Setup

1. Navigate to the config service directory:
   ```bash
   cd config-service
   ```

2. Configure the Git repository location in `application.yml`:
   ```yaml
   spring:
     cloud:
       config:
         server:
           git:
             uri: ${CONFIG_REPO_URI:your-config-repo-url}
   ```

3. Alternatively, use a local filesystem:
   ```yaml
   spring:
     cloud:
       config:
         server:
           native:
             search-locations: classpath:/config
   ```

### Service-Specific Configuration

Each microservice should have its configuration file in the config repository:

- `discovery-service.yml`
- `gateway-service.yml`
- `conference-service.yml`
- `keynote-service.yml`

## Running the Application

Follow this specific order to start the services:

### 1. Start Config Service
```bash
cd config-service
mvn spring-boot:run
```
Wait for the service to fully start (check logs for "Started ConfigServiceApplication").

### 2. Start Discovery Service
```bash
cd discovery-service
mvn spring-boot:run
```
Access Eureka Dashboard at: `http://localhost:8761`

### 3. Start Gateway Service
```bash
cd gateway-service
mvn spring-boot:run
```
The gateway will be available at: `http://localhost:8888`

### 4. Start Business Services

Start these in any order:

**Conference Service**:
```bash
cd conference-service
mvn spring-boot:run
```

**Keynote Service**:
```bash
cd keynote-service
mvn spring-boot:run
```

### 5. Start Angular Frontend
```bash
cd management-app-angular
npm install
ng serve
```
Access the application at: `http://localhost:4200`

### Docker Compose (Alternative)

If Docker Compose configuration is available:
```bash
docker-compose up -d
```

## API Documentation

### Gateway Endpoints

All requests should go through the API Gateway at `http://localhost:8888`

### Conference Service Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/conferences` | Get all conferences |
| GET | `/api/conferences/{id}` | Get conference by ID |
| POST | `/api/conferences` | Create new conference |
| PUT | `/api/conferences/{id}` | Update conference |
| DELETE | `/api/conferences/{id}` | Delete conference |

### Keynote Service Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/keynotes` | Get all keynotes |
| GET | `/api/keynotes/{id}` | Get keynote by ID |
| POST | `/api/keynotes` | Create new keynote |
| PUT | `/api/keynotes/{id}` | Update keynote |
| DELETE | `/api/keynotes/{id}` | Delete keynote |

### Service Discovery

Check registered services at: `http://localhost:8761`

## Project Structure

```
Conference_Management_System/
├── config-service/              # Centralized configuration server
│   ├── src/
│   └── pom.xml
├── discovery-service/           # Eureka service registry
│   ├── src/
│   └── pom.xml
├── gateway-service/             # API Gateway
│   ├── src/
│   └── pom.xml
├── conference-service/          # Conference management
│   ├── src/
│   └── pom.xml
├── keynote-service/             # Keynote speaker management
│   ├── src/
│   └── pom.xml
├── management-app-angular/      # Frontend application
│   ├── src/
│   ├── angular.json
│   └── package.json
├── mvnw                         # Maven wrapper
├── mvnw.cmd                     # Maven wrapper (Windows)
├── pom.xml                      # Parent POM
└── README.md
```

## Development Guidelines

### Adding a New Microservice

1. Create a new Spring Boot module
2. Add Eureka client dependency
3. Configure service name in `application.yml`
4. Register routes in Gateway Service
5. Add configuration to Config Service

### Best Practices

- Always register services with Eureka
- Use the Config Service for all configurations
- Route all external requests through the Gateway
- Implement proper error handling and logging
- Use DTOs for data transfer between services
- Implement circuit breakers for resilience
- Write unit and integration tests

## Monitoring and Health Checks

- **Eureka Dashboard**: `http://localhost:8761`
- **Gateway Actuator**: `http://localhost:8888/actuator/health`
- **Service Health**: `http://localhost:8888/{service-name}/actuator/health`

## Troubleshooting

### Services not registering with Eureka
- Ensure Discovery Service is running first
- Check network connectivity
- Verify `eureka.client.service-url.defaultZone` configuration

### Configuration not loading
- Verify Config Service is running
- Check Git repository connectivity
- Review application name matches configuration file name

### Gateway routing issues
- Verify service is registered with Eureka
- Check Gateway route configurations
- Review service URLs in gateway configuration

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is available for educational and commercial use. Please refer to the LICENSE file for details.

## Contact

**Developer**: Ayoub Ouhensous  
**Repository**: [Conference_Management_System](https://github.com/ayoubouhensous/Conference_Management_System)

---

## Acknowledgments

- Spring Boot and Spring Cloud communities
- Netflix OSS for Eureka
- Angular team for the excellent frontend framework

## Future Enhancements

- [ ] Implement authentication and authorization with Spring Security
- [ ] Add email notification service
- [ ] Integrate payment gateway for conference fees
- [ ] Add real-time chat/messaging functionality
- [ ] Implement document management for paper submissions
- [ ] Add analytics and reporting dashboard
- [ ] Implement mobile applications (iOS/Android)
- [ ] Add multi-language support
- [ ] Implement calendar integration
- [ ] Add video conferencing integration for virtual conferences

