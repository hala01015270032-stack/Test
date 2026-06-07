# 🛍️ ECommerce Platform

> A modern, scalable e-commerce API built with C# and clean architecture principles

![C#](https://img.shields.io/badge/Language-C%23-239120?style=flat-square&logo=csharp)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-green?style=flat-square)

---

## 📋 Table of Contents

- [🚀 Project Overview](#project-overview)
- [🏗️ Architecture Overview](#architecture-overview)
- [⚙️ Environment Configuration](#environment-configuration)
- [📡 API Documentation](#api-documentation)
- [📦 Setup Instructions](#setup-instructions)
- [🤝 Contributing](#contributing)
- [📄 License](#license)

---

## 🚀 Project Overview

This is a comprehensive **E-Commerce Platform API** designed to handle modern online shopping requirements. Built with C# and following industry best practices, it provides a robust foundation for building scalable, maintainable e-commerce solutions.

### Key Features ✨

- 🔐 **Secure Authentication & Authorization**
- 📦 **Product Management System**
- 🛒 **Shopping Cart & Order Management**
- 💳 **Payment Processing Integration**
- 📊 **Analytics & Reporting**
- 🔄 **Inventory Management**
- 👥 **User Management**

---

## 🏗️ Architecture Overview

This project follows the **Clean Architecture** pattern with a layered approach, ensuring separation of concerns and maintainability.

### Project Structure

```
ECommerce/
├── ECommerce.API/              # 🌐 Presentation Layer (REST API Endpoints)
│   ├── Controllers/            # API Controllers
│   ├── Models/                 # Request/Response DTOs
│   └── Configuration/          # API Configuration & Middleware
│
├── ECommerce.Application/      # 🔧 Application Layer (Business Logic)
│   ├── Services/               # Business Logic Services
│   ├── DTOs/                   # Data Transfer Objects
│   ├── Mapping/                # AutoMapper Profiles
│   └── Validators/             # Request Validators
│
├── ECommerce.Domain/           # 📐 Domain Layer (Core Business Rules)
│   ├── Entities/               # Core Business Entities
│   ├── ValueObjects/           # Value Objects
│   ├── Exceptions/             # Domain Exceptions
│   └── Interfaces/             # Repository & Service Contracts
│
├── ECommerce.Infrastructure/   # 💾 Infrastructure Layer (Data Access)
│   ├── Persistence/            # Database Context & Migrations
│   ├── Repositories/           # Data Access Implementation
│   ├── Services/               # External Service Implementations
│   └── Configuration/          # Infrastructure Setup
│
└── Database/                   # 🗂️ Database Scripts & Documentation
    ├── Migrations/             # EF Core Migrations
    └── Seeds/                  # Initial Data Seeds
```

### Architecture Diagram

```
┌─────────────────────────────────────────────────────┐
│         API Controllers (HTTP Endpoints)            │ ← ECommerce.API
├─────────────────────────────────────────────────────┤
│    Application Services (Business Logic)            │ ← ECommerce.Application
├──────────────────────���──────────────────────────────┤
│    Domain Models (Core Business Rules)              │ ← ECommerce.Domain
├─────────────────────────────────────────────────────┤
│    Repositories & External Services                 │ ← ECommerce.Infrastructure
├─────────────────────────────────────────────────────┤
│         SQL Server Database                         │ ← Database
└─────────────────────────────────────────────────────┘
```

### Design Patterns Used 🎯

- **Repository Pattern**: Data access abstraction
- **Dependency Injection**: Loose coupling and testability
- **SOLID Principles**: Clean and maintainable code
- **MVC/MVVM**: Separation of concerns
- **Factory Pattern**: Object creation abstraction
- **Observer Pattern**: Event handling

---

## ⚙️ Environment Configuration

### Prerequisites 📋

- **.NET SDK**: 6.0 or higher
- **SQL Server**: 2019 or higher (or SQL Server Express)
- **Visual Studio**: 2022 Community/Professional or VS Code with C# extensions
- **Git**: Latest version

### Environment Variables

Create an `appsettings.json` file in the `ECommerce.API` project:

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=YOUR_SERVER;Database=ECommerceDB;User Id=sa;Password=YOUR_PASSWORD;"
  },
  "Jwt": {
    "Key": "your-secret-key-min-32-characters-long",
    "Issuer": "ecommerce-api",
    "Audience": "ecommerce-client",
    "ExpirationMinutes": 60
  },
  "Email": {
    "SmtpServer": "smtp.gmail.com",
    "SmtpPort": 587,
    "SenderEmail": "your-email@gmail.com",
    "SenderPassword": "your-app-password"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning"
    }
  }
}
```

### Development Environment Setup 🛠️

```bash
# Set environment variable
set ASPNETCORE_ENVIRONMENT=Development
```

### Production Environment Setup 🚀

```bash
# Set environment variable
set ASPNETCORE_ENVIRONMENT=Production
```

---

## 📡 API Documentation

### Base URL

```
https://api.yourdomain.com/api/v1
```

### Authentication 🔐

All protected endpoints require a **JWT Bearer Token** in the Authorization header:

```
Authorization: Bearer <your_jwt_token>
```

### Core API Endpoints

#### 👥 Authentication Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---|
| `POST` | `/auth/register` | Register new user | ❌ |
| `POST` | `/auth/login` | Login user | ❌ |
| `POST` | `/auth/refresh-token` | Refresh JWT token | ❌ |
| `POST` | `/auth/logout` | Logout user | ✅ |

#### 📦 Products Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---|
| `GET` | `/products` | Get all products | ❌ |
| `GET` | `/products/{id}` | Get product by ID | ❌ |
| `GET` | `/products/category/{categoryId}` | Get products by category | ❌ |
| `POST` | `/products` | Create new product | ✅ |
| `PUT` | `/products/{id}` | Update product | ✅ |
| `DELETE` | `/products/{id}` | Delete product | ✅ |

#### 🛒 Cart Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---|
| `GET` | `/cart` | Get user cart | ✅ |
| `POST` | `/cart/items` | Add item to cart | ✅ |
| `PUT` | `/cart/items/{itemId}` | Update cart item | ✅ |
| `DELETE` | `/cart/items/{itemId}` | Remove item from cart | ✅ |
| `DELETE` | `/cart/clear` | Clear entire cart | ✅ |

#### 📋 Orders Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---|
| `GET` | `/orders` | Get user orders | ✅ |
| `GET` | `/orders/{id}` | Get order details | ✅ |
| `POST` | `/orders` | Create new order | ✅ |
| `PUT` | `/orders/{id}/status` | Update order status | ✅ |
| `DELETE` | `/orders/{id}` | Cancel order | ✅ |

#### 🏷️ Categories Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---|
| `GET` | `/categories` | Get all categories | ❌ |
| `GET` | `/categories/{id}` | Get category by ID | ❌ |
| `POST` | `/categories` | Create category | ✅ |
| `PUT` | `/categories/{id}` | Update category | ✅ |
| `DELETE` | `/categories/{id}` | Delete category | ✅ |

### Response Format

#### Success Response (200 OK)

```json
{
  "success": true,
  "message": "Operation completed successfully",
  "data": {
    "id": 1,
    "name": "Product Name",
    "price": 99.99
  }
}
```

#### Error Response (400/500)

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": [
    {
      "field": "email",
      "message": "Invalid email format"
    }
  ]
}
```

---

## 📦 Setup Instructions

### Step 1️⃣: Clone the Repository

```bash
git clone https://github.com/hala01015270032-stack/Test.git
cd Test
```

### Step 2️⃣: Install Dependencies

```bash
# Restore NuGet packages
dotnet restore
```

### Step 3️⃣: Configure Environment

1. Copy `appsettings.json.example` to `appsettings.json`
2. Update database connection string
3. Configure JWT settings
4. Set up email credentials (optional)

### Step 4️⃣: Setup Database

```bash
# Navigate to Infrastructure project
cd ECommerce.Infrastructure

# Apply migrations
dotnet ef database update --startup-project ../ECommerce.API

# Seed initial data (optional)
dotnet ef database update --migration AddInitialData --startup-project ../ECommerce.API
```

### Step 5️⃣: Run the Application

```bash
# From project root
cd ECommerce.API
dotnet run
```

The API will be available at: `https://localhost:5001`

### Step 6️⃣: Verify Installation ✅

```bash
# Test the API
curl https://localhost:5001/api/v1/products
```

---

## 🧪 Testing

### Running Unit Tests

```bash
# Run all tests
dotnet test

# Run specific test project
dotnet test ECommerce.Application.Tests

# Run with verbose output
dotnet test --verbosity detailed
```

### Running Integration Tests

```bash
dotnet test --filter "Category=Integration"
```

---

## 📖 Documentation

### API Swagger Documentation

When running locally, visit:
```
https://localhost:5001/swagger
```

Swagger UI provides interactive API documentation with the ability to test endpoints directly.

### Architecture Decision Records

See `/docs/ADR/` for architecture decisions and rationale.

---

## 🤝 Contributing

We welcome contributions! Please follow these steps:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'Add some AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

### Code Standards 📝

- Follow C# naming conventions (PascalCase for classes, camelCase for variables)
- Write unit tests for new features
- Update documentation
- Ensure code compiles without warnings

---

## 🐛 Troubleshooting

### Common Issues

**Issue**: Database connection fails
- **Solution**: Verify connection string in `appsettings.json` and ensure SQL Server is running

**Issue**: JWT token invalid
- **Solution**: Ensure JWT secret key is correctly configured and token hasn't expired

**Issue**: CORS errors
- **Solution**: Check CORS policy in `Startup.cs` allows your client origin

---

## 📞 Support & Contact

For questions or issues:
- 📧 Email: `support@ecommerce.dev`
- 🐛 Issues: [GitHub Issues](https://github.com/hala01015270032-stack/Test/issues)
- 💬 Discussions: [GitHub Discussions](https://github.com/hala01015270032-stack/Test/discussions)

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Built with [.NET](https://dotnet.microsoft.com/)
- Database management with [Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/)
- API documentation with [Swagger/OpenAPI](https://swagger.io/)
- Dependency injection with [Microsoft.Extensions.DependencyInjection](https://docs.microsoft.com/en-us/dotnet/core/extensions/dependency-injection)

---

<div align="center">

**Made with ❤️ by the Development Team**

⭐ If you find this project helpful, please consider giving it a star!

</div>
