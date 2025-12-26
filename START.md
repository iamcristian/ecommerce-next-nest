# 🚀 Getting Started - E-Commerce System

## 📋 Prerequisites

- **Node.js** 22+ (check with `node -v`)
- **pnpm** 9+ (install: `npm install -g pnpm`)
- **Docker Desktop** installed and running
- **Git** configured

---

## ⚡ Quick Start (Local Development)

### 1️⃣ Clone Repository

```bash
git clone git@github.com:iamcristian/ecommerce-next-nest.git
cd ecommerce-system
```

### 2️⃣ Setup Environment Variables

```bash
# Copy example file
cp .env.example .env

# Edit .env if needed (optional for development)
```

### 3️⃣ Start Services (PostgreSQL only)

```bash
# Start infrastructure services
docker-compose -f docker-compose.dev.yml up -d

# Verify they're running
docker-compose -f docker-compose.dev.yml ps
```

You should see:

- ✅ `ecommerce-postgres-dev` (healthy)

### 4️⃣ Install Dependencies and Run Apps

#### Terminal 1 - Backend (NestJS)

```bash
cd server
pnpm install
pnpm start:dev
```

You should see: `Nest application successfully started on http://localhost:3001`

#### Terminal 2 - Frontend (Next.js)

```bash
cd client
pnpm install
pnpm dev
```

You should see: `Ready in 2.5s on http://0.0.0.0:3002`

### 5️⃣ Verify Everything Works

Open your browser and check:

- **Frontend**: http://localhost:3002
- **Backend Health**: http://localhost:3001/health

---

## 🔄 Daily Workflow

```bash
# 1. Start services (once or when you restart your PC)
docker-compose -f docker-compose.dev.yml up -d

# 2. Work on code (changes reflect automatically)
# - Edit files in server/ or client/
# - Hot-reload works instantly

# 3. When done, stop services (optional)
docker-compose -f docker-compose.dev.yml stop
```

---

## 🛠️ Useful Command

### Docker (Services)

```bash
# View service logs
docker-compose -f docker-compose.dev.yml logs -f postgres

# Stop services
docker-compose -f docker-compose.dev.yml stop

# Stop and remove (keeps volumes/data)
docker-compose -f docker-compose.dev.yml down

# Reset everything (DELETES DATABASE DATA)
docker-compose -f docker-compose.dev.yml down -v

# Check status
docker-compose -f docker-compose.dev.yml ps

# Restart specific service
docker-compose -f docker-compose.dev.yml restart postgres
```

### Backend (NestJS)

```bash
cd server

# Desarrollo
pnpmvelopment
pnpm start:dev          # Hot-reload

# Testing
pnpm test               # Unit tests
pnpm test:watch         # Watch mode
pnpm test:cov           # Coverage
pnpm test:e2e           # E2E tests

# Linting
pnpm lint               # Check
pnpm lint --fix         # Fix

# Build
pnpm build              # Build for production
```

### Frontend (Next.js)

```bash
cd client

# Development
pnpm dev                # Hot-reload

# Testing (when added)
pnpm test

# Linting
pnpm lint               # Check

# Build
pnpm build              # Build for production
pnpm start              # Run production build
```

---

## 🐳 Production Mode (Everything in Docker)

To test full production environment:

```bash
# Build and run everything in Docker
docker-compose up -d --build

# View logs
docker-compose logs -f

# Stop
docker-compose down

# URLs (same ports but different configuration)
# - Frontend: http://localhost:3002
# - Backend: http://localhost:3001
```

**Differences from dev mode:**

- Uses optimized builds (multi-stage)
- No hot-reload
- Simulates real production environment
- Slower for code changes

---

## 🔍 Troubleshooting

### "Puerto ya en uso"

ort already in use"

```bash
# Check what's using the port
lsof -i :3001  # Mac/Linux
netstat -ano | findstr :3001  # Windows

# Stop Docker services
docker-compose -f docker-compose.dev.yml down
```

### "Cannot connect to database"

```bash
# Verify PostgreSQL is running
docker-compose -f docker-compose.dev.yml ps

# View postgres logs
docker-compose -f docker-compose.dev.yml logs postgres

# Restart postgres
docker-compose -f docker-compose.dev.yml restart postgres
```

### "pnpm: command not found"

```bash
# Install pnpm globally
npm install -g pnpm

# Verify installation
pnpm -v
```

### Reset Database

```bash
# Stop services and remove volumes
docker-compose -f docker-compose.dev.yml down -v

# Start again
docker-compose -f docker-compose.dev.yml up -d
```

---

## �️ Using Adminer (Database UI)

Adminer is a web-based database management tool (like phpMyAdmin but lighter).

### Access Adminer

1. Make sure Docker services are running:

```bash
docker-compose -f docker-compose.dev.yml ps
```

2. Open in browser: http://localhost:8080

3. Login with these credentials:
   - **System**: `PostgreSQL`
   - **Server**: `postgres`
   - **Username**: `postgres`
   - **Password**: `postgres123`
   - **Database**: `ecommerce_dev`

### What You Can Do with Adminer

- **Browse tables**: Click database name → Select table
- **Run SQL queries**: Click "SQL command" → Type query → Execute
- **View data**: Click table name to see all rows
- **Insert/Edit data**: Click "New item" or edit icon
- **Export database**: Click "Export" for backup
- **Import SQL**: Click "Import" to restore/seed data
- **Check schema**: See table structure, indexes, foreign keys

### Common Tasks

**See all tables:**

```sql
SELECT tablename FROM pg_tables WHERE schemaname = 'public';
```

**Check if database is empty:**
Just browse the database - if no tables appear, it's empty (normal on first run)

**Create test data:**
Use "SQL command" to insert sample records

### Tips

- Adminer auto-reconnects if PostgreSQL restarts
- Use it instead of installing pgAdmin or DBeaver
- Perfect for quick checks during development
- Tables will appear here after running migrations

---

## �📊 Port Structure

| Service            | Port | URL                   |
| ------------------ | ---- | --------------------- |
| Frontend (Next.js) | 3002 | http://localhost:3002 |
| Backend (NestJS)   | 3001 | http://localhost:3001 |
| PostgreSQL         | 5432 | localhost:5432        |

---

## 🎯 Complete Workflow Example

```bash
# 1. Start of day
docker-compose -f docker-compose.dev.yml up -d

# 2. Terminal 1 - Backend
cd server
pnpm start:dev

# 3. Terminal 2 - Frontend
cd client
pnpm dev

# 4. Terminal 3 - Git commands, tests, etc.
git checkout -b feature/new-feature

# ... work on code ...

# 5. Before commit
cd server && pnpm lint && pnpm test
cd ../client && pnpm lint

# 6. Commit and push
git add .
git commit -m "feat: new feature"
git push origin feature/new-feature

# 7. End of day (optional)
docker-compose -f docker-compose.dev.yml stop
```

---

## 📚 Additional Resources

- **Project documentation**: See `/docs` folder
- **NestJS**: https://docs.nestjs.com
- **Next.js**: https://nextjs.org/docs
- **Docker Compose**: https://docs.docker.com/compose

---

## 💡 Pro Tips

1. **Hot-reload**: Any change in `server/src/` or `client/app/` reflects automatically
2. **Adminer**: Use it to inspect DB without external tools
3. **VSCode**: Install recommended extensions for better DX
4. **Git**: Commit frequently in feature branches
5. **Tests**: Run tests before every important commit
6. **Database**: Use pgAdmin or DBeaver to inspect PostgreSQL if needed

---

## ❓ Support

If you have problems:

1. Check this guide
2. Verify logs: `docker-compose -f docker-compose.dev.yml logs`
3. Search `/docs` for additional documentation
4. Open an issue o
