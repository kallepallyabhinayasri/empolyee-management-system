# PeopleDesk Employee Management System

A lightweight employee management application with a static HTML/CSS/JavaScript frontend, an Express API, and Supabase as its database and authentication provider.

## Requirements

- Node.js 18 or newer
- A Supabase project

## Setup

1. In Supabase, open **SQL Editor** and run `backend/database/schema.sql`. Optionally run `backend/database/seed.sql` to add sample departments and employees.
2. To use Supabase, create an account in Supabase Authentication (email/password). To associate the account with an employee record, set that user's auth UUID in `employees.auth_user_id`.
3. Copy `.env.example` to `.env`. Add the Supabase project URL and **service role** key from Project Settings → API. Keep `.env` private; never put the service role key in frontend code. If `.env` is absent during local development, the server starts in clearly labeled demo mode instead.
4. Install and start the app:

   ```sh
   npm install
   npm run dev
   ```

5. Open `http://localhost:3000` and sign in with the Supabase account, or use `demo@peopledesk.local` / `Demo123!` in local demo mode. Demo changes are stored in memory and reset when the server restarts. If you open the HTML with VS Code Live Server or as a local file, API calls are directed to Express at `http://localhost:3000`; the Express server must still be running.

For a frontend hosted at a different API address, set `window.PEOPLEDESK_API_URL` before loading `js/app.js` (for example, `http://localhost:3000/api`). The server permits local development origins and can be configured with a comma-separated `FRONTEND_ORIGIN` allowlist for production.

## Features

- Dashboard summary and department overview
- Search, add, edit, and remove employee records
- Add, edit, and remove departments
- Supabase email/password sign-in and current-user profile
- API token verification using Supabase Auth

## API

All API routes except `POST /api/auth/login` and `GET /api/health` require `Authorization: Bearer <access-token>`.

- `GET /api/auth/me`
- `GET|POST /api/employees`
- `GET|PUT|DELETE /api/employees/:id`
- `GET|POST /api/departments`
- `PUT|DELETE /api/departments/:id`

The server serves the frontend and API on the same origin. Direct frontend file opening is not supported because sign-in and API calls require the server.
