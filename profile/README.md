# Effort Lab

## Overview

Effort Lab is a coaching platform that helps trainers provide structured feedback through effort cards. The platform consists of three main components: a backend API, a web application, and a mobile application.

## Architecture

```
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│   Web App       │  │   Mobile App    │  │   Backend API   │
│   Next.js 15    │  │   React Native  │  │   Go 1.23       │
│   TypeScript    │  │   Expo SDK 53   │  │   PostgreSQL    │
└─────────────────┘  └─────────────────┘  └─────────────────┘
         │                     │                     │
         └─────────────────────┼─────────────────────┘
                               │
                    ┌─────────────────┐
                    │   Fly.io        │
                    │   Deployment    │
                    └─────────────────┘
```

## Repositories

### [API Services](./api)
**Backend API built with Go**
- RESTful API with JWT authentication (phone-based)
- Background job processing with Asynq
- PostgreSQL database with GORM ORM
- Redis for caching and job queues
- OpenAI integration for AI-powered features
- Deployed on Fly.io with separate API and worker services

### [Web Application](./webapp)
**Admin dashboard for trainers**
- Next.js 15 with App Router
- TypeScript with strict mode
- Tailwind CSS v4 for styling
- OAuth authentication (Google/Apple planned)
- Admin-only access control
- Static site generation for marketing pages

### [Mobile App](./native)
**Cross-platform mobile application**
- React Native with Expo SDK 53
- Expo Router for file-based navigation
- NativeWind for Tailwind CSS styling
- TypeScript throughout
- Phone authentication flow
- Support for iOS and Android

## Tech Stack

### Backend
- Go 1.23
- PostgreSQL (primary database)
- Redis (caching, job queue)
- Asynq (background jobs)
- Fiber (HTTP framework)
- GORM (ORM)
- JWT authentication
- Casbin (authorization)

### Frontend
- Next.js 15
- React 19
- TypeScript 5.3
- Tailwind CSS 4
- Zustand (state management)
- Axios (API client)

### Mobile
- React Native 0.76
- Expo SDK 53
- Expo Router 5
- NativeWind 4
- TypeScript
- React Query (data fetching)
- Zustand (state management)

### Infrastructure
- Fly.io (hosting)
- Upstash Redis
- Tigris (S3-compatible storage)
- GitHub Actions (CI/CD)
- Docker (containerization)

## Development Setup

### Prerequisites
- Go 1.23+
- Node.js 20+
- PostgreSQL 15+
- Redis 7+

### API Development
```bash
cd api
cp .env.example .env
go mod download
air  # Hot reload development server
```

### Web Development
```bash
cd webapp
npm install
npm run dev  # Development server at localhost:3000
```

### Mobile Development
```bash
cd native
npm install
npm run start  # Expo development server
npm run ios    # iOS simulator
npm run android  # Android emulator
```

## Testing

### API
```bash
cd api
./scripts/test-full.sh  # Unit and E2E tests
./scripts/lint-fast.sh  # Linting
./scripts/scan.sh       # Security scan
```

### Web
```bash
cd webapp
npm run lint   # ESLint and Prettier
npm run check  # TypeScript type checking
```

### Mobile
```bash
cd native
npm test              # Jest tests
npm run type-check    # TypeScript checking
npm run lint          # ESLint and Prettier
```

## Deployment

### Environments
- **Development**: dev.effortlab.io
- **Staging**: staging.effortlab.io  
- **Production**: effortlab.io

### API Deployment (Fly.io)
```bash
cd api
# Development
fly deploy --app effortlab-api-dev --config deployment/development/fly.api.toml
fly deploy --app effortlab-worker-dev --config deployment/development/fly.worker.toml

# Production
fly deploy --app effortlab-api-prod --config deployment/production/fly.api.toml
fly deploy --app effortlab-worker-prod --config deployment/production/fly.worker.toml
```

## API Documentation

- Swagger UI available at `/swagger/index.html` on each API environment
- Authentication required in staging/production environments
- OpenAPI spec at `/docs/swagger.json`

## Contributing

Each repository contains:
- `CLAUDE.md` - Development guidelines and patterns
- `.github/` - GitHub Actions workflows
- Environment-specific configuration files

Submit PRs with:
- Passing tests
- Linter compliance
- Updated documentation where applicable
