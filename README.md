# InvNexus

InvNexus is a minimal microservice-based inventory and sales management system built for learning and demonstrating modern backend architecture patterns using .NET and Azure.

The project focuses on:

- Clean Architecture
- CQRS
- JWT Authentication
- Microservices
- Azure Deployment
- Azure Key Vault
- Azure Functions
- CI/CD-ready structure

---

# Architecture Overview

```text
Client Application
        |
        v
---------------------
|   Auth Service    |
---------------------
        |
      JWT
        |
        v
-------------------------
|   Inventory Service   |
-------------------------
        |
        |---- Product Management
        |---- Stock Management
        |---- Order Creation
        |---- Order Cancellation
        |---- Sales Tracking
        |
        v
---------------------------
| Notification Service    |
---------------------------
        |
        v
Azure Function (Retry Failed Notifications)
```

---

# Services

## 1. InvNexus.AuthService

Handles authentication and authorization.

### Features

- User login
- JWT token generation
- Role-based authorization
- Secure service authentication
- Azure Key Vault integration

### Tech

- ASP.NET Core Web API
- JWT Authentication
- SQL Server
- Azure Key Vault

---

## 2. InvNexus.InventoryService

Core business service for inventory and order processing.

### Features

- Product CRUD
- Stock management
- Create order
- Cancel order
- Sales record generation
- CQRS implementation

### Business Flow

```text
Create Order
    ↓
Validate Stock
    ↓
Reduce Stock
    ↓
Create Sales Record
    ↓
Send Notification
```

### Cancel Order Flow

```text
Cancel Order
    ↓
Restore Stock
    ↓
Update Order Status
    ↓
Send Notification
```

### Tech

- ASP.NET Core Web API
- Clean Architecture
- CQRS
- Entity Framework Core
- SQL Server

---

## 3. InvNexus.NotificationService

Handles notification processing and logging.

### Features

- Notification logging
- Order created notification
- Order cancelled notification
- Failed notification tracking

### Tech

- ASP.NET Core Web API
- MongoDB (optional)
- REST communication

---

## 4. InvNexus.Functions

Background processing using Azure Functions.

### Features

- Retry failed notifications
- Scheduled background jobs

### Example

```text
Timer Trigger:
Runs every 10 minutes
Checks failed notifications
Retries sending notifications
```

---

# Technology Stack

| Category | Technology |
|---|---|
| Backend | .NET 8 Web API |
| Language | C# |
| Architecture | Clean Architecture |
| Pattern | CQRS |
| Database | SQL Server |
| Optional Database | MongoDB |
| Authentication | JWT |
| Cloud | Microsoft Azure |
| Hosting | Azure App Service |
| Secrets Management | Azure Key Vault |
| Background Jobs | Azure Functions |
| Source Control | GitHub |

---

# Azure Components

| Azure Service | Purpose |
|---|---|
| Azure App Service | Host APIs |
| Azure SQL Database | Store transactional data |
| Azure Key Vault | Store secrets securely |
| Azure Functions | Background processing |
| Application Insights | Monitoring and logging |

---

# Solution Structure

```text
InvNexus/
|
|-- services/
|    |
|    |-- InvNexus.AuthService
|    |-- InvNexus.InventoryService
|    |-- InvNexus.NotificationService
|    |-- InvNexus.Functions
|
|-- shared/
|    |
|    |-- BuildingBlocks
|    |-- SharedKernel
|
|-- docs/
|    |
|    |-- architecture
|    |-- api
|    |-- deployment
|
|-- docker/
|
|-- README.md
```

---

# Future Enhancements

- API Gateway
- Docker Compose
- Kubernetes deployment
- Event-driven communication
- Redis caching
- OpenTelemetry tracing
- CI/CD pipeline
- Role-based dashboard UI

---

# Goal of the Project

This project is intended for:

- Learning cloud-native backend development
- Practicing Azure deployment
- Demonstrating architecture skills
- Building a portfolio-ready GitHub project
- Exploring scalable backend design patterns
