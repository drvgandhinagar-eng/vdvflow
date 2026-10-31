# FORGEFLOW

Manufacturing progress and godown tracking system. This repository contains one Next.js application with separate Admin and Worker portals, sharing one PostgreSQL database.

## Features

- Admin and Worker authentication with role-based access
- Manufacturing order and item creation
- Per-item manufacturing stage routes
- Worker assignments and production submissions
- Admin approval/rejection of production updates
- Piece and weight recording
- Manual bundle creation with accepted-quantity checks
- Bundle dispatch and godown receipt confirmation
- Item-wise CSV report export (opens in Excel)
- Activity log for important actions

## Requirements

- Node.js 20.9 or later
- PostgreSQL 14 or later
- npm

## Run locally

1. Extract the project ZIP.
2. Open a terminal in the `forgeflow` folder.
3. Install packages:

   ```bash
   npm install
   ```

4. Create a PostgreSQL database named `forgeflow`.
5. Copy `.env.example` to `.env` and set your database connection:

   ```env
   DATABASE_URL="postgresql://postgres:YOUR_PASSWORD@localhost:5432/forgeflow?schema=public"
   AUTH_SECRET="use-a-long-random-secret-value"
   ```

6. Create the database tables:

   ```bash
   npx prisma migrate dev --name init
   ```

7. Create the initial demo users:

   ```bash
   npm run db:seed
   ```

8. Start the website:

   ```bash
   npm run dev
   ```

9. Open http://localhost:3000

## Initial demo login credentials

**Admin portal**
- Username: `forgeadmin`
- Password: `ForgeFlow@Admin2026!`

**Worker portal**
- Username: `forgeworker`
- Password: `ForgeFlow@Worker2026!`

The seed script creates these users and hashes their passwords. These are demo credentials only. Change them before deploying for real factory use. Never commit your `.env` file or production secrets to GitHub.

## Publish to GitHub

Create an empty repository on GitHub. Then run these commands from the project folder:

```bash
git init
git add .
git commit -m "Initial FORGEFLOW manufacturing tracking system"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

Replace the remote URL with your own GitHub repository URL.

## Build for production

```bash
npm run build
npm run start
```

You must configure a hosted PostgreSQL database and environment variables on your hosting provider before deployment.

## Important implementation notes

- Production submissions are pending until an Admin approves or rejects them.
- Approved production updates contribute to the approved quantity total.
- Bundle creation is restricted to accepted, not-yet-bundled pieces.
- A bundle is only marked received after the Admin confirms the receipt.
- The standard stage route is created for each new item. The schema supports per-item routes.
- The report currently exports CSV, which can be opened in Microsoft Excel.

## Current scope

This is a practical first version focused on manufacturing tracking. It is not a full ERP. Before using it for live factory operations, perform acceptance testing with realistic sample orders and review the business rules with the factory team.
