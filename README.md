# Orderbook Project

This repository contains a multi-service orderbook trading system built with TypeScript, PostgreSQL/TimescaleDB, Redis, WebSocket, REST API, and a Next.js frontend.

## Repository Structure

- `api/` - REST API service for orderbook endpoints and market data.
- `db/` - Database service for seeding, database access, and refresh tasks.
- `engine/` - Orderbook engine service with matching and orderbook snapshot support.
- `mm/` - Market-making / helper service that interacts with the engine ecosystem.
- `ws/` - WebSocket service for real-time subscriptions and user messaging.
- `frontend/` - Next.js frontend application for trading UI, depth charts, and market data.
- `docker/` - Docker Compose configuration for TimescaleDB and Redis.

## Prerequisites

- Node.js 18+ or compatible
- npm
- Docker and Docker Compose (for local TimescaleDB and Redis)

## Local Setup

### 1. Start infrastructure

From the `docker/` directory:

```bash
cd docker
docker compose up -d
```

This starts:

- `timescaledb` on port `5432`
- `redis` on port `6379`

### 2. Install dependencies

Install dependencies in each package directory:

```bash
cd api && npm install
cd ../db && npm install
cd ../engine && npm install
cd ../mm && npm install
cd ../ws && npm install
cd ../frontend && npm install
```

### 3. Build services

Most services use TypeScript and require a build step.

```bash
cd api && npm run build
cd ../db && npm run build
cd ../engine && npm run build
cd ../mm && npm run build
cd ../ws && npm run build
cd ../frontend && npm run build
```

## Running Services

### REST API

```bash
cd api
npm run start
```

### Database service

Seed or refresh data with:

```bash
cd db
npm run seed:db
npm run refresh:views
```

### Engine service

```bash
cd engine
npm run start
```

The engine service reads its snapshot data when started with `WITH_SNAPSHOT=true`.

### Market-maker service

```bash
cd mm
npm run start
```

### WebSocket service

```bash
cd ws
npm run start
```

### Frontend

```bash
cd frontend
npm run dev
```

Then open the frontend in your browser at `http://localhost:3000`.

## Development Notes

- `api/` exposes HTTP endpoints and connects to Redis and PostgreSQL.
- `ws/` handles real-time subscription management and user WebSocket connections.
- `engine/` is the matching engine and orderbook logic.
- `db/` manages database seeding and cron-style refresh tasks.
- `frontend/` is built with Next.js and Tailwind CSS.

## TODOs

These TODO notes were present in the repository:

- Add a balances endpoint.
- Implement fiat on-ramp for users.
- Capture additional DB events beyond trades (orders, ticker updates).
- Add engine and orderbook tests.
- Let users subscribe to their own trade fills.

## Notes

- The root repository does not contain a single top-level package manager file; each service is managed independently.
- Use Docker Compose to ensure Redis and PostgreSQL/TimescaleDB are available before starting the services.
