# 🚀 AI Product Finder

AI Product Finder is a full-stack AI-powered product recommendation platform that allows users to search for products using natural language, compare products using AI, manage wishlists, track search history, and access personalized features through secure authentication.

The application is built using **React, Spring Boot, PostgreSQL, Spring Security, JWT, OpenRouter AI, Docker, Nginx, and AWS EC2** and is deployed as a production-ready containerized application on AWS.

---

# 🔗 Project Links

### 🌐 Live Application

https://13.205.5.209/

### 💻 Frontend Repository

https://github.com/LavanyaSriChava/ai-product-finder-frontend

### ⚙️ Backend Repository

https://github.com/LavanyaSriChava/ai-product-finder-Backend

---

# ✨ Features

## 🤖 AI Product Recommendation

- AI-powered product search using natural language
- Personalized product recommendations
- OpenRouter API integration
- LLM-generated product specifications and recommendations
- Public product search support

## ⚖️ AI Product Comparison

- Compare products using AI
- Feature-by-feature comparison
- Analyze specifications and use cases
- AI-generated recommendation verdict

## 🔐 Authentication & Authorization

- User registration
- User login
- JWT-based authentication
- Stateless Spring Security
- Role-Based Access Control (RBAC)
- User and Admin roles
- BCrypt password hashing

## ❤️ Wishlist Management

- Add products to wishlist
- Remove products from wishlist
- View saved products
- User-specific wishlist persistence

## 📜 Search History

- Automatically stores searches for authenticated users
- View previous searches
- Delete individual search records
- Clear complete search history

## 👨‍💼 Admin Dashboard

- Admin-only protected routes
- Platform monitoring
- Search analytics
- User insights

## 📖 API Documentation

- Swagger / OpenAPI documentation
- Interactive REST API testing
- JWT Bearer Authentication support

## 🐳 Containerization

- Multi-stage Docker build
- Dockerized Spring Boot application
- Dockerized PostgreSQL database
- Docker Compose orchestration
- Persistent PostgreSQL volume
- Automatic container restart policy

---

# 🏗️ Tech Stack

## Frontend

- React.js
- React Router
- Axios
- Tailwind CSS
- Vite

## Backend

- Java 17
- Spring Boot
- Spring MVC
- Spring Data JPA
- Hibernate

## Security

- Spring Security
- JWT Authentication
- BCrypt Password Encoder
- Role-Based Access Control

## Database

- PostgreSQL 17

## AI Integration

- OpenRouter API
- Large Language Models (LLMs)
- Prompt-based product recommendation

## API Development

- RESTful APIs
- DTO Pattern
- Global Exception Handling
- Swagger / OpenAPI

## DevOps & Cloud

- Docker
- Docker Compose
- AWS EC2
- AWS Elastic IP
- Nginx
- Let's Encrypt
- Certbot
- HTTPS/TLS

## Build Tools

- Maven
- Vite / npm

---

# ☁️ AWS Deployment Architecture

The complete application is deployed on an **AWS EC2 instance**.

```text
                         Internet
                            │
                            │ HTTPS
                            ▼
                  ┌──────────────────┐
                  │   AWS Elastic IP │
                  │   13.205.5.209   │
                  └────────┬─────────┘
                           │
                           ▼
                  ┌──────────────────┐
                  │      Nginx       │
                  │ Reverse Proxy +  │
                  │ Static Hosting   │
                  └───────┬──────────┘
                          │
               ┌──────────┴──────────┐
               │                     │
               ▼                     ▼
         React Frontend        /api/* Requests
         Static Build                │
                                     ▼
                           ┌──────────────────┐
                           │   Spring Boot    │
                           │ Docker Container │
                           │     :8080        │
                           └────────┬─────────┘
                                    │
                       ┌────────────┴────────────┐
                       │                         │
                       ▼                         ▼
              PostgreSQL Database         OpenRouter API
               Docker Container             AI / LLM
                    :5432
```

### Request Flow

```text
User
  ↓
HTTPS
  ↓
AWS Elastic IP
  ↓
Nginx
  ├── /       → React Frontend
  │
  └── /api/*  → Spring Boot Backend
                      ↓
               PostgreSQL
                      +
               OpenRouter API
```

Nginx acts as the public entry point and reverse proxy for the application.

---

# 🔒 HTTPS Configuration

The production application is secured using HTTPS.

TLS certificates are issued using **Let's Encrypt** and managed through **Certbot**.

```text
Client
   ↓ HTTPS
Nginx
   ↓
Spring Boot
```

Certificate renewal is configured automatically through Certbot.

---

# 📂 Backend Project Structure

```text
src/main/java/com/lavanya/aiproductfinder
│
├── controller
├── service
│   └── impl
├── repository
├── entity
├── dto
├── security
├── exception
├── enums
└── config
```

---

# 🔐 User Roles

## Guest

Can:

- Search for products using AI

## Registered User

Can:

- Search products
- Compare products
- Manage wishlist
- Access search history

## Admin

Can:

- Access user features
- Access protected admin functionality
- View platform analytics

---

# 📡 Main API Endpoints

## Authentication

```http
POST /api/auth/register
POST /api/auth/login
```

## AI

```http
POST /api/ai/search
POST /api/ai/compare
```

## Wishlist

```http
GET    /api/wishlist
POST   /api/wishlist
DELETE /api/wishlist/{id}
```

## Search History

```http
GET    /api/search-history
DELETE /api/search-history/{id}
DELETE /api/search-history/clear
```

## Admin

```http
GET /api/admin/dashboard
```

Protected endpoints require:

```http
Authorization: Bearer <JWT_TOKEN>
```

---

# 🐳 Docker Deployment

The backend and PostgreSQL database are containerized using Docker and orchestrated with Docker Compose.

## Services

```text
docker-compose.yml
│
├── backend
│   └── Spring Boot
│
└── postgres
    └── PostgreSQL 17
```

PostgreSQL data is stored using a persistent Docker volume.

## Build and Start

```bash
docker compose up -d --build
```

## View Running Containers

```bash
docker compose ps
```

## View Backend Logs

```bash
docker logs ai-product-finder
```

## Stop Containers

```bash
docker compose down
```

---

# 💻 Running Locally

## Prerequisites

Install:

- Java 17+
- Maven
- Docker
- Node.js
- npm

Clone the backend:

```bash
git clone https://github.com/LavanyaSriChava/ai-product-finder-Backend.git
cd ai-product-finder-Backend
```

Create a `.env` file containing the required environment variables.

Example:

```env
POSTGRES_DB=your_database
POSTGRES_USER=your_username
POSTGRES_PASSWORD=your_password
OPENROUTER_API_KEY=your_openrouter_api_key
```

> Never commit `.env` files, database credentials, API keys, JWT secrets, or other sensitive credentials to GitHub.

Start the application:

```bash
docker compose up -d --build
```

Backend:

```text
http://localhost:8080
```

Swagger UI:

```text
http://localhost:8080/swagger-ui/index.html
```

---

# 🚀 Production Deployment

| Component | Deployment |
|---|---|
| Frontend | AWS EC2 + Nginx |
| Backend | AWS EC2 + Docker |
| Database | PostgreSQL 17 + Docker |
| Reverse Proxy | Nginx |
| Public Networking | AWS Elastic IP |
| HTTPS | Let's Encrypt + Certbot |
| AI Service | OpenRouter API |

### Production URL

```text
https://13.205.5.209/
```

The production API is accessed through Nginx:

```text
https://13.205.5.209/api/*
```

---

# 🛡️ Production Reliability

The AWS deployment includes:

- Persistent PostgreSQL Docker volume
- Automatic Docker container restart policy
- Nginx reverse proxy
- HTTPS encryption
- Automatic TLS certificate renewal
- AWS Elastic IP for a stable public endpoint
- Swap memory configured on the EC2 instance
- Environment-based secret management

---

# 🔑 Environment Variables

Sensitive configuration is provided through environment variables rather than being hardcoded into the source code.

Examples include:

```text
POSTGRES_DB
POSTGRES_USER
POSTGRES_PASSWORD
OPENROUTER_API_KEY
```

The `.env` file is excluded from Git using `.gitignore`.

---

# 📌 Deployment Highlights

This project demonstrates:

- Full-stack application development
- REST API design
- JWT authentication and authorization
- AI/LLM API integration
- Relational database persistence
- Docker containerization
- Multi-container orchestration
- AWS EC2 deployment
- Nginx reverse proxy configuration
- HTTPS/TLS configuration
- Production environment management

---

# 👨‍💻 Author

**Lavanya Chava**

GitHub:  
https://github.com/LavanyaSriChava

LinkedIn:  
https://linkedin.com/in/lavanya-sri-chava-6b57a02a9

---

⭐ If you found this project interesting, consider giving it a star.
