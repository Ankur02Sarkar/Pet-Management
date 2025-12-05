# Pet Management Backend (Next.js + Motia)

A production-ready backend for managing pets, built with Next.js and Motia. It combines fast HTTP APIs, background processing, workflow orchestration, AI-assisted decisions, and real-time streaming to deliver a modern, scalable system.

## Features

- Pet CRUD via HTTP endpoints
- Adoption workflow (quarantine → health checks → availability)
- Feeding reminders with scheduled jobs
- AI-assisted health decisions and recommendations
- Cleanup jobs for soft-deleted pets
- Real-time streaming updates from workflows and jobs

## Stack

- Framework: `Next.js` (TypeScript)
- Backend orchestration: `Motia`
- Runtime: `Node.js v18+`

## Quick Start

1. Ensure `Node.js v18+` is installed.
2. Install dependencies:
   - `npm install`
3. Start development:
   - `npm run dev`
4. Open the Motia Workbench to interactively test API steps, jobs, workflows, and streams.

> Motia handles APIs, jobs, workflows, AI agents, and streams in a single project with minimal setup—no separate services required.

## Core Concepts

### API Endpoints

- Define API Steps to handle requests and return proper HTTP responses.
- Validate all inputs with schemas to enforce predictable data.
- Test endpoints directly in Workbench.

Example operations:

- `GET /api/pets` — list pets
- `POST /api/pets` — create pet
- `PUT /api/pets/:id` — update pet
- `DELETE /api/pets/:id` — soft-delete pet

### Background Jobs

- Event Steps trigger from APIs to run async tasks.
- Cron Steps run on schedules (e.g., feeding reminders, cleanup).
- Monitor jobs in Workbench with clear execution history.

### Workflows

- Build orchestrators that coordinate complex processes.
- Support automatic and manual transitions between states.
- Enforce state validation and progression rules.

Adoption workflow example:

- `received → quarantine → health_check → available`

### AI Agents

- Generate content and make decisions as part of workflows.
- Use agents to evaluate symptoms and recommend treatments.
- Integrate agentic routing for dynamic process flows.

### Real-Time Streaming

- Define stream configurations to push updates to clients.
- APIs can return immediately while background steps stream progress.
- Jobs and AI agents can publish status and enrichment events.
- Multiple steps can write to the same stream for a unified client view.

## API Overview

These are representative endpoints; adapt as your implementation evolves.

- `GET /api/pets` — Paginated list of pets
- `POST /api/pets` — Create a new pet
- `GET /api/pets/:id` — Retrieve a pet
- `PUT /api/pets/:id` — Update a pet
- `DELETE /api/pets/:id` — Soft-delete a pet
- `POST /api/adoptions/:id/start` — Kick off adoption workflow
- `POST /api/pets/:id/feeding/schedule` — Configure feeding reminders

Authentication: Use `Authorization: Bearer <token>` for protected endpoints. Public endpoints should be explicitly designated.

## Development

- Run local server: `npm run dev`
- Use Workbench to:
  - Validate request schemas
  - Trigger event and cron steps
  - Observe workflow transitions
  - Inspect real-time streams

### Example cURL

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <token>" \
  -d '{"name":"Bella","species":"dog"}' \
  http://localhost:3000/api/pets
```

## Security

- Default to zero-trust: authenticate and authorize all requests unless public.
- Validate all inputs via schemas; reject invalid payloads.
- Never log secrets or sensitive data.

## Project Structure (example)

```
src/
  app/                 # Next.js app routes
  server/              # API handlers and Motia step bindings
  workflows/           # Motia workflow orchestrators
  jobs/                # Event and cron steps
  agents/              # AI agents for decisions and content
  streams/             # Stream configurations
```

## Testing & Monitoring

- Test endpoints and steps interactively in Workbench.
- Use real-time streams to monitor long-running processes.
- Review execution logs and state transitions for workflows.

## Deployment

- Deploy the Next.js app to your preferred platform (e.g., Vercel).
- Motia components run within the same project—no separate services required.

## Reference

- Learn Motia by building a pet store backend covering APIs, jobs, workflows, AI agents, and real-time streaming.
