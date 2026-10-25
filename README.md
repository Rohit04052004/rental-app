# RentIful — Rental Property Management App

A full-stack rental property platform where managers can list properties and tenants can search, favorite, and apply for them. Built by **Rohit Chigatapu**.

## What this app does

- **Tenants** can search and filter rental listings (price, beds/baths, amenities, location radius on a map), save favorites, submit rental applications, and track their leases and payments.
- **Managers** can list new properties (with photo uploads), review and approve/deny applications, and manage their existing listings.
- Authentication and role-based access (tenant vs. manager) via AWS Cognito.
- Property locations are geocoded and queried with PostGIS for radius-based search, and rendered on an interactive Mapbox map.

## Tech stack

**Client** (`/client`)
- Next.js 15 (App Router) + React 19 + TypeScript
- Redux Toolkit / RTK Query for state & data fetching
- Tailwind CSS + shadcn/ui (Radix primitives)
- AWS Amplify (Cognito-backed auth)
- Mapbox GL for maps

**Server** (`/server`)
- Node.js + Express + TypeScript
- Prisma ORM over PostgreSQL with the PostGIS extension (geospatial queries)
- AWS S3 for property photo storage
- JWT-based authorization middleware (validates Cognito-issued tokens)

## Project structure

```
client/   Next.js frontend
server/   Express API + Prisma schema/migrations/seed data
```

## Getting started

### Prerequisites

- Node.js 18+
- A PostgreSQL database with the PostGIS extension enabled
- An AWS account (S3 bucket for photos, Cognito user pool for auth)
- A Mapbox access token

### Server setup

```bash
cd server
npm install
# create server/.env with DATABASE_URL, AWS_REGION, S3_BUCKET_NAME, AWS credentials, PORT
npx prisma migrate dev
npm run seed      # optional: loads sample properties/tenants/managers
npm run dev
```

### Client setup

```bash
cd client
npm install
# create client/.env.local with NEXT_PUBLIC_API_BASE_URL, NEXT_PUBLIC_AWS_COGNITO_USER_POOL_ID,
# NEXT_PUBLIC_AWS_COGNITO_USER_POOL_CLIENT_ID, NEXT_PUBLIC_MAPBOX_TOKEN
npm run dev
```

The client runs on `http://localhost:3000` and expects the API server (default port `3002`) to be reachable at `NEXT_PUBLIC_API_BASE_URL`.

## Credits

Adapted from an open-source rental platform tutorial project, maintained and extended here by Rohit Chigatapu.
