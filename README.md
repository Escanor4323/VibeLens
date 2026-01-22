<div align="center">
  <img src="docs/gdg-google-developer-group-logo.svg" alt="Google Developer Group C" width="400"/>
  
  # VibeLens
</div>

> A music recommendation API built with TypeScript and NestJS, demonstrating secure, scalable, AI-ready backend systems using Hexagonal Architecture and vector-based recommendations.

---

## 🚀 Overview

VibeLens is a production-ready API that enables applications to authenticate users securely, ingest music tracks, generate vector embeddings, and provide intelligent music recommendations based on similarity and user taste.

This project serves two primary purposes:

1. **Hands-on Workshop** - Learn authentication, clean architecture, and recommendation systems through guided implementation
2. **Reference Backend** - A production-ready foundation for building real-world music personalization services

---

## ✨ Features

### Authentication
- Email & password registration with secure password hashing
- JWT access tokens (short-lived) and refresh tokens (long-lived)
- Session-based token management with rotation
- Protected endpoints with role-based access control
- Social login support (Google, Apple, Facebook)

### Music Recommendation Engine
- Vector-based similarity search for music tracks
- Cosine distance computation for recommendations
- User taste modeling and session-based recommendations
- AI-ready architecture supporting multiple embedding sources
- Pluggable vector store integration

### Architecture
- **Hexagonal Architecture (Ports & Adapters)** - Clean separation of concerns
- **Domain-Driven Design** - Business logic independent of infrastructure
- **Testable by Design** - Unit, integration, and E2E testing support
- **Infrastructure Agnostic** - Swap databases, frameworks, or vendors without changing business logic

---

## 🏗️ Architecture

VibeLens follows **Hexagonal Architecture** (also known as Ports & Adapters), ensuring that business logic remains independent of external systems.

```
HTTP Controller (Adapter)
      ↓
Application Service
      ↓
Domain Layer (Business Logic)
      ↓
Repository Port (Interface)
      ↓
Infrastructure Adapter (PostgreSQL / Vector Store)
```

### Key Principles

- **Domain Independence**: The domain layer has zero knowledge of:
  - Databases or ORMs
  - JWT libraries
  - Web frameworks
  - External services
- **Port-Based Communication**: All external systems communicate through well-defined ports (interfaces)
- **Swappable Infrastructure**: Change databases, vector stores, or frameworks without modifying business logic
- **Testability**: Domain logic is unit-testable without infrastructure dependencies

---

## 📁 Project Structure

The project is organized by feature and architectural responsibility:

```
src/
├── auth/                    # Authentication bounded context
│   ├── domain/             # Auth domain entities
│   ├── dto/                # Data transfer objects
│   ├── infrastructure/      # Repository implementations
│   ├── strategies/         # JWT validation strategies
│   ├── auth.service.ts     # Business logic
│   ├── auth.controller.ts # HTTP endpoints
│   └── auth.module.ts      # NestJS module
│
├── music/                  # Music recommendation bounded context
│   ├── domain/             # Music domain entities
│   ├── dto/                # Request/response DTOs
│   ├── infrastructure/     # Vector store adapters
│   ├── music.service.ts    # Recommendation logic
│   ├── music.controller.ts # HTTP endpoints
│   └── music.module.ts     # NestJS module
│
├── users/                  # User management
├── session/                # Session management
└── shared/                  # Shared utilities and types
```

Each feature:
- Defines its own domain boundaries
- Exposes repository ports (interfaces)
- Implements infrastructure adapters
- Exposes APIs through versioned controllers

---

## 🧰 Tech Stack

| Category | Technology |
|----------|-----------|
| **Language** | TypeScript |
| **Framework** | NestJS |
| **Architecture** | Hexagonal (Ports & Adapters) |
| **Authentication** | JWT (access + refresh tokens) |
| **Database** | PostgreSQL (relational data) |
| **Vector Search** | Pluggable vector database |
| **Containerization** | Docker & Docker Compose |
| **Validation** | class-validator, class-transformer |
| **API Documentation** | Swagger/OpenAPI |

---

## 🚀 Quick Start

### Prerequisites

- Node.js >= 16.0.0
- Docker & Docker Compose
- npm >= 8.0.0

### Installation

1. **Clone the repository**

```bash
git clone git@github.com:Escanor4323/VibeLens.git
cd VibeLens
```

2. **Set up environment**

```bash
cp env-example-relational .env
```

Edit `.env` and configure:
- Database connection (use `localhost` when running locally)
- JWT secrets and expiration times
- Mail server settings

3. **Start infrastructure**

```bash
docker compose up -d postgres adminer maildev
```

4. **Install dependencies**

```bash
npm install
```

5. **Run migrations and seeds**

```bash
npm run migration:run
npm run seed:run:relational
```

6. **Start the development server**

```bash
npm run start:dev
```

The API will be available at:
- **API**: http://localhost:3000
- **Swagger Docs**: http://localhost:3000/docs
- **Database Admin**: http://localhost:8080

---

## 📚 Documentation

- [Workshop Guide: Authentication](./docs/workshop-auth.md) - Step-by-step guide to implementing JWT authentication
- [Architecture Overview](./docs/architecture.md) - Deep dive into Hexagonal Architecture
- [Database Setup](./docs/database.md) - Database configuration and migrations
- [Testing Guide](./docs/tests.md) - Testing strategies and examples

---

## 🧪 Testing Philosophy

VibeLens is built with testability as a first-class concern:

- **Unit Tests**: Domain logic tested in isolation
- **Integration Tests**: Services tested with mocked ports
- **E2E Tests**: Full API workflows tested end-to-end
- **No Infrastructure Required**: Domain tests don't need databases or external services

Because of architectural separation, you can test business logic without spinning up the entire stack.

---

## 🧑‍🏫 Workshop-Friendly Design

This repository is intentionally structured for learning:

- **Incremental Implementation**: Missing code fails with helpful error messages
- **Step-by-Step Guides**: Each section teaches a clear architectural lesson
- **Self-Contained Examples**: Each feature demonstrates a specific pattern
- **Production-Ready Result**: The final implementation is a fully working API

Perfect for:
- University workshops and courses
- Internal engineering training
- Self-guided learning
- Code review and architecture discussions

---

## 🔐 Security Considerations

- **No PHI in Tokens**: JWT payloads contain only user ID, role, and session ID
- **Password Hashing**: bcrypt with salt for secure password storage
- **Token Rotation**: Refresh tokens are rotated on every use
- **Session Management**: Server-side session tracking for revocation
- **Input Validation**: All requests validated with class-validator
- **HTTPS Ready**: Designed for production HTTPS deployment

---

## 🔮 Future Extensions

VibeLens is intentionally extensible. Possible extensions include:

- **User Taste Embeddings**: Model user preferences as vectors
- **Collaborative Filtering**: Recommendations based on similar users
- **Playlist Generation**: Automatic playlist creation
- **Real-Time Feedback**: Live recommendation updates
- **Event-Driven Architecture**: Async ingestion and processing
- **OAuth Providers**: Additional social login options
- **Rate Limiting**: Abuse protection and throttling
- **A/B Testing**: Recommendation algorithm experimentation

---

## 🎯 Who Is This For?

- **Backend Engineers** learning system design and clean architecture
- **Full-Stack Developers** exploring recommendation systems
- **Students** studying software architecture and design patterns
- **Engineering Teams** adopting Hexagonal Architecture
- **Workshop Instructors** teaching backend development

---

## 🤝 Contributing

Contributions are welcome! Please read our contributing guidelines and code of conduct before submitting pull requests.

---

## 📜 License

MIT License - feel free to use this project for learning, teaching, and building.

---

## 🙏 Acknowledgments

Built on top of the excellent [NestJS Boilerplate](https://github.com/brocoders/nestjs-boilerplate) by Brocoders, adapted for music recommendation and educational purposes.

---

**Built with ❤️ for the developer community**
