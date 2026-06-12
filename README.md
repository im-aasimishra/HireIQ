# HireIQ Project Foundation

This is the full-stack foundation of **HireIQ**, a modern hiring platform built with Next.js, FastAPI, and a specialized database pipeline to handle relations, caches, unstructured data, vector search, and skill graphing.

---

## Technical Stack

### Frontend
- **Framework**: Next.js 14 (App Router)
- **Language**: TypeScript
- **Styling**: Tailwind CSS & shadcn/ui components
- **State Management**: Zustand
- **Data Fetching**: React Query (TanStack Query)
- **Forms**: React Hook Form with Zod validation
- **Authentication**: NextAuth

### Backend
- **Framework**: FastAPI (Python 3.12)
- **ORM & Migrations**: SQLAlchemy & Alembic

### Infrastructure
- Docker & Docker Compose

### Databases
1. **PostgreSQL** (Port `5432`) - User profiles, application states, and relational tables.
2. **Redis** (Port `6379`) - Active sessions, user metadata cache, and rate-limiting.
3. **MongoDB** (Port `27017`) - Semi-structured resume data storage, JSON dumps from parsers.
4. **Qdrant** (Port `6333` / `6334`) - Dense vector indexes for semantic matching between resumes and job specs.
5. **Neo4j** (Port `7474` / `7687`) - Skill graph paths and competency dependency graphs.

---

## Directory Structure

```
hireiq/
├── docker-compose.yml
├── .env.example
├── README.md
├── frontend/
│   ├── Dockerfile
│   ├── package.json
│   ├── tsconfig.json
│   ├── tailwind.config.ts
│   ├── postcss.config.js
│   ├── next.config.mjs
│   └── src/
│       ├── app/ (App Router layouts, pages, API handlers)
│       ├── components/ (shadcn/ui & dashboard panels)
│       ├── store/ (Zustand store for app state)
│       └── lib/ (Query Client & utilities)
└── backend/
    ├── Dockerfile
    ├── requirements.txt
    ├── alembic.ini
    └── app/
        ├── main.py (FastAPI entrypoint)
        ├── core/ (Settings, database connector engines)
        ├── db/ (Mongo, Redis, Qdrant, Neo4j connection classes)
        └── api/ (FastAPI health endpoints checking all 5 databases)
```

---

## Getting Started

### Prerequisites
- Docker & Docker Compose
- Node.js 18+ (for running frontend locally)
- Python 3.12 (for running backend locally)

### Setup Configurations
1. Copy the environment variables template:
   ```bash
   cp .env.example .env
   ```
2. Adjust environment configs in `.env` if executing services outside Docker.

### Spin Up Databases and Services
Run the entire platform via Docker Compose:
```bash
docker compose up --build
```
This command starts all 5 databases, builds and exposes the FastAPI backend on port `8000`, and starts the Next.js app on port `3000`.

- **Frontend**: http://localhost:3000
- **Backend API Docs**: http://localhost:8000/docs
- **Health Check Endpoint**: http://localhost:8000/api/v1/health
