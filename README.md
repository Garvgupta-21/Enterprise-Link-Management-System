# Enterprise Link Management System

**Enterprise Link Management System** is a full-stack link management platform for creating branded short URLs, tracking engagement, and managing links from one clean dashboard.

Built as a portfolio-ready application, it combines a responsive React interface with a secure Node.js API, PostgreSQL persistence, Redis caching, and background click-event processing.

## Highlights

- Create short links with optional custom aliases, expiry dates, and privacy controls
- Secure account creation and sign-in with JWT authentication and bcrypt password hashing
- Manage, pause, edit, delete, and copy links from a single dashboard
- Track clicks, QR scans, referrers, devices, browsers, and geographic data
- Generate customizable QR codes and export them as PNG or SVG
- Import up to 50 URLs at once from a CSV file
- Protect the API with validation, URL-safety checks, and token-bucket rate limiting

## Tech stack

| Area | Technology |
| --- | --- |
| Frontend | React 18, Vite, Recharts, Lucide, PapaParse |
| Backend | Node.js, Express, Zod, JWT, bcrypt |
| Data | PostgreSQL 16, Redis 7 |
| Background jobs | BullMQ |
| Deployment | Docker Compose, Nginx |

## Architecture

```text
React + Nginx (port 80)
          |
          v
Express API (port 5000) <--> Redis cache and BullMQ
          |
          v
     PostgreSQL database
```

## Run with Docker

### Requirements

- Docker Desktop for Windows, macOS, or Linux

### Start the application

From the project folder, run:

```bash
docker compose up --build -d
```

Then open [http://localhost](http://localhost).

Useful local endpoints:

| Service | Address |
| --- | --- |
| Link Management app | `http://localhost` |
| API health check | `http://localhost:5000/health` |
| PostgreSQL | `localhost:5432` |
| Redis | `localhost:6379` |

To stop the containers:

```bash
docker compose down
```

## Run without Docker

1. Start PostgreSQL and Redis locally.
2. Copy `backend/.env.example` to `backend/.env` and set a strong `JWT_SECRET`.
3. Copy `frontend/.env.example` to `frontend/.env` and set `VITE_API_BASE_URL=http://localhost:5000`.
4. Install dependencies:

```bash
npm --prefix backend install
npm --prefix frontend install
```

5. Start the API, worker, and frontend in three separate terminals:

```bash
npm --prefix backend start
```

```bash
npm --prefix backend run worker
```

```bash
npm --prefix frontend run dev
```

The frontend development server is available at `http://localhost:5173`.

## Key API routes

| Method | Route | Purpose |
| --- | --- | --- |
| `POST` | `/api/auth/signup` | Create an account |
| `POST` | `/api/auth/login` | Start an authenticated session |
| `POST` | `/api/shorten` | Create a short URL |
| `GET` | `/api/my-links` | List the signed-in user’s links |
| `PUT` | `/api/links/:id` | Update a link |
| `DELETE` | `/api/links/:id` | Delete a link |
| `GET` | `/api/stats/:shortCode/analytics` | Retrieve link analytics |
| `GET` | `/health` | Check API, database, and Redis status |

## Resume description

> Built **Enterprise Link Management System**, a full-stack URL management and analytics platform using React, Node.js, PostgreSQL, Redis, and Docker. Implemented JWT authentication, custom links, QR generation, CSV imports, async click processing, and engagement dashboards.

## License

MIT
