# E-Commerce System - Next.js + NestJS

Sistema de e-commerce completo con arquitectura fullstack moderna.

## Stack Tecnológico

- **Frontend**: Next.js 15, React 19, TailwindCSS 4
- **Backend**: NestJS, TypeScript
- **Database**: PostgreSQL 15
- **Cache**: Redis
- **Containerización**: Docker + Docker Compose

## Desarrollo Local

### Opción 1: Desarrollo Híbrido (RECOMENDADO) ⚡

Ejecuta solo servicios en Docker, apps corren localmente con hot-reload nativo:

```bash
# 1. Levantar servicios (PostgreSQL, Redis)
docker-compose -f docker-compose.dev.yml up -d

# 2. En terminal 1 - Backend
cd server
pnpm install
pnpm start:dev

# 3. En terminal 2 - Frontend
cd client
pnpm install
pnpm dev
```

**Ventajas:**

- ⚡ Hot-reload instantáneo
- 🐛 Debugging nativo
- 💾 Menos consumo de recursos
- 🚀 Más rápido que Docker

**URLs:**

- Frontend: http://localhost:3002
- Backend: http://localhost:3001
- Adminer (DB UI): http://localhost:8080

### Opción 2: Todo en Docker

Para simular entorno de producción:

```bash
docker-compose up -d
```

| Service    | URL                   | Description        |
| ---------- | --------------------- | ------------------ |
| Client     | http://localhost:3002 | Next.js Frontend   |
| Server     | http://localhost:3001 | NestJS Backend API |
| PostgreSQL | localhost:5432        | Database           |

### Health Check Endpoints

- **Server**: http://localhost:3001/health
- **Client**: http://localhost:3002/api/health

### Useful Docker Commands

```bash
# View logs
docker-compose logs -f

# View logs for specific service
docker-compose logs -f server
docker-compose logs -f client

# Stop all services
docker-compose down

# Stop and remove volumes (clean database)
docker-compose down -v

# Rebuild a specific service
docker-compose up --build server
```

## Local Development (Without Docker)

### Prerequisites

- Node.js 22+
- pnpm

### Server (NestJS)

```bash
cd server
pnpm install
pnpm start:dev
```

### Client (Next.js)

```bash
cd client
pnpm install
pnpm dev
```

## Running Tests

```bash
# Server tests
cd server
pnpm test

# Client lint
cd client
pnpm lint
```

## Features

### Essential Features:

- User authentication and authorization (sign-up, login, roles: admin/seller/customer, JWT & OAuth2).
- Product catalog with categories and search functionality.
- Shopping cart and checkout process (Stripe).
- Order management (view orders, order status updates).
- Reviews and ratings for products.
- Dashboard for sellers to manage their products and view sales analytics.
- Admin dashboard for managing products, orders, and users.

### Future Features:

- Wishlist functionality.
- Multi-language and multi-currency support.
- Analytics dashboard for admins.
- Notifications (email, SMS, or push notifications).

## Tech Stack

### Frontend:

- Framework: Next.js (React-based framework).
- Styling: TailwindCSS, Shadcn.
- State Management: Zustand.
- Icons: lucide.dev.
- Graphics: Recharts.
- Validation: Zod.

### Backend:

- Framework: NestJS (Node.js framework).
- Database: PostgreSQL (SQLite in development).
- Authentication: JWT (JSON Web Tokens) & Google OAuth2.
- API: RESTful.
- Payment Integration: Stripe.
- Hashing: bcrypt.
- Documentation: Swagger.

### Testing:

- Frontend: Vitest, Playwright.
- Backend: Jest, Supertest.

### DevOps:

- Containerization: Docker & Docker Compose.
- CI/CD: GitHub Actions.
- Deployment: Thinking.

## Installation and Setup

### Prerequisites:

- Node.js, pnpm, Docker.

### Steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/ecommerce-system.git
   ```
2. Go to the client/server directory:

```bash
 cd client/server
```

3. Install dependencies:
   ```bash
   pnpm install
   ```
4. Start the development servers:
   - Frontend:
     ```bash
     pnpm dev
     ```
   - Backend:
     ```bash
     pnpm start:dev
     ```

## Contact

- **Name**: Cristian Arando
- **Email**: crisarandosyse@gmail.com
- **LinkedIn**: [Cristian Arando](https://linkedin.com/in/cristian-arando)
- **Portfolio**: [Cristian Arando Portfolio](https://cristianarando.netlify.app/en)
