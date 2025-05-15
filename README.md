# GettingStartedCleanArchitectureProject

# Getting Started – Clean Architecture Project

This guide will help you set up and run the project on your local machine for development and testing purposes.

---

## Prerequisites

Before starting, ensure you have the following tools installed:

| **Tool**         | **Description**                            | **Link**                                                                 |
|------------------|--------------------------------------------|--------------------------------------------------------------------------|
| [.NET SDK]       | Required to build and run the app          | [Download](https://dotnet.microsoft.com/download)                        |
| [Git]            | Version control system                     | [Download](https://git-scm.com/downloads)                                |
| [EF Core CLI]    | For database migrations (if applicable)    | [Install Guide](https://learn.microsoft.com/en-us/ef/core/cli/dotnet)    |
| Visual Studio or VS Code | Recommended IDE                     | [VS 2022](https://visualstudio.microsoft.com/) / [VS Code](https://code.visualstudio.com/) |

---

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repository.git
cd your-repository
```
Note: Replace your-username/your-repository with the actual GitHub path.

### 2. Restore NuGet Packages
Restore all dependencies:
```bash
dotnet restore
```

### 3. Configure the Database (Optional if using EF Core)
Edit the appsettings.json (or appsettings.Development.json) with your local database connection string:

```bash
"ConnectionStrings": {
  "DefaultConnection": "Server=localhost;Database=YourDbName;User Id=sa;Password=your_password;"
}
```
Note: Ensure your database server (e.g., SQL Server or PostgreSQL) is running locally or accessible.

### 5. Run the Application
Run the main project (usually the one containing your Startup.cs or Program.cs):

```bash
dotnet run --project src/YourMainProject
```
Note: Replace src/YourMainProject with the actual path to your .csproj file.

### 6. Test the API
Once the app is running, open your browser and visit:
- Swagger UI: https://localhost:5001/swagger
- Health Check (if implemented): https://localhost:5001/health

### 7. Run Unit Tests (If available)
```bash
dotnet test
```
Note: This will discover and run all test projects and output the results in the terminal.

### (Optional) Run with Docker
If the solution provides Docker support:

```bash
docker-compose up --build
```
Note: Make sure docker and docker-compose are installed and running.

---

## Project Structure Overview

```bash
📦 Root
├── 🧠 Domain
│   ├── DomainEvents
│   ├── Entities
│   ├── Enumerators
│   ├── Constants
│   ├── Exceptions
│   ├── Repositories
│   ├── Shared
│   └── ValueObjects
│
├── 📋 Application
│   ├── Abstractions
│   │   ├── Data
│   │   ├── Email
│   │   └── Messaging
│   ├── Behaviors
│   ├── Contracts
│   ├── User
│   │   ├── Commands
│   │   └── Queries
│   ├── Order
│   │   ├── Commands
│   │   └── Queries
│   └── UseCases *(optional)*
│
├── 🏗 Infrastructure
│   ├── Data
│   │   ├── Repositories
│   │   ├── Migrations
│   │   └── DataContext
│   │       └── ApplicationDbContext.cs
│   ├── Messaging
│   ├── Services
│   └── Jobs
│
└── 🌐 Presentation
    ├── Controllers
    ├── Middlewares
    ├── Extensions
    ├── DTOs
    ├── Endpoints *(Minimal APIs – optional)*
    └── ViewModels *(optional for UI rendering)*
```

### Architecture Principles
This project follows the Clean Architecture approach:
- Domain Layer: Pure C# domain logic, no dependencies.
- Application Layer: Use cases, interfaces, and CQRS with MediatR.
- Infrastructure Layer: Technical implementations (e.g., database, messaging).
- Presentation Layer: API controllers, middleware, and endpoints.

### Additional Notes
Environment-specific configuration is handled via .json files and/or environment variables.

- Secrets can be managed with:
  - dotnet user-secrets (local development)
  - Azure Key Vault or AWS Secrets Manager (production)

- This solution uses:
  - MediatR for request/response handling
  - FluentValidation for model validation
  - Serilog or equivalent for structured logging




