# STP — Student Budget Planner

STP (Student Budget Planner) is a student-focused budgeting application built with React, TypeScript, TanStack Start, Supabase, and Tailwind CSS. The current source includes income, expense, budget, savings, recurring transaction, and statement workflows. The AI Coach and Settings screens are placeholders and require further implementation.

## Requirements

- Node.js 20 or newer (use the current LTS release)
- npm
- A Supabase project for authentication and persistent data

## Local setup

1. Clone the repository and open its folder in VS Code.
2. Install dependencies: `npm install`
3. Copy `.env.example` to `.env` and fill in your own Supabase project URL and publishable/anon key.
4. Start the development server: `npm run dev`
5. Open the local URL printed by Vite (normally `http://localhost:3000`).

## Supabase configuration

The app uses Supabase Auth and Postgres. Apply the SQL schema in `drizzle/migrations/0000_migration.sql` to your Supabase database, then configure Row Level Security policies appropriate for your project. The current AI Coach and Settings screens are intentionally marked as placeholders in the source; a Gemini API key alone will not activate AI features until a server-side Gemini feature is implemented. Never expose a Supabase service-role key in browser code or commit it to Git.

For Google sign-in, enable Google under Supabase Dashboard → Authentication → Providers → Google. Add your Supabase Auth callback URL to the Google OAuth client's authorized redirect URIs. Add your local and production app URLs to Supabase Authentication → URL Configuration → Redirect URLs. The app's Google sign-in redirects back to the current app origin.

Email/password registration, login, password reset, and session persistence use Supabase Auth directly.

## Environment variables

| Variable | Where used |
|---|---|
| `VITE_SUPABASE_URL` | Browser Supabase client |
| `VITE_SUPABASE_PUBLISHABLE_KEY` | Browser Supabase client (publishable/anon key only) |
| `SUPABASE_URL` | Server-side Supabase operations |
| `SUPABASE_PUBLISHABLE_KEY` | Server-side user-authenticated operations |
| `SUPABASE_SERVICE_ROLE_KEY` | Optional server-only admin operations; keep secret |
| `GEMINI_API_KEY` | Reserved for a future server-side AI integration; not used by the current AI Coach placeholder |

## Commands

- `npm run dev` — local development
- `npm run build` — production build and TypeScript check
- `npm run start` — run the built Nitro server
- `npm run test` — run tests
- `npm run lint` — lint source files

## Deployment

The app uses TanStack Start with Nitro. For Vercel, import the GitHub repository, use `npm install` as the install command and `npm run build` as the build command. Configure the environment variables above in Vercel Project Settings. Set the production URL in Supabase Auth URL Configuration and Google OAuth settings.

## Security notes

- `.env` is ignored by Git. Never commit real secrets.
- `VITE_` variables are bundled into browser code; only Supabase publishable/anon keys belong there.
- Never put `SUPABASE_SERVICE_ROLE_KEY`, Google OAuth client secrets, or Gemini API keys in client-side code.
- Configure and test Row Level Security for every user-owned table before using real financial data.

## Branding

Product name: **STP — Student Budget Planner**.
Tagline: **Smart Money. Smarter Students.**
