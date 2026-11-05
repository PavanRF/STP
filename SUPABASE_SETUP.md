# STP Supabase setup

The local `.env` file is configured with the Supabase project URL and publishable key supplied for this STP project. The publishable key is intended for client-side use. Do not add a service-role/secret key to any `VITE_` variable or commit `.env`.

## 1. Create the database schema

1. Open the Supabase project: `https://supabase.com/dashboard/project/khorvlzkjjdenvbzxfxs`.
2. Open **SQL Editor** and create a new query.
3. Paste the contents of `supabase/migrations/20261105000000_initial_schema.sql` and run it once.
4. Confirm the tables `profiles`, `income`, `expenses`, `budgets`, `savings_goals`, `savings_contributions`, `recurring_rules`, and `ai_insights` exist under **Table Editor**.

The SQL creates per-user Row Level Security policies and a profile-creation trigger. Run it only on a new/empty STP database. If you already ran it, do not run it again without checking for existing tables/policies.

## 2. Configure authentication

In Supabase **Authentication → URL Configuration**, set the Site URL to your local app URL while developing (`http://localhost:3000`). Add these Redirect URLs:

- `http://localhost:3000/**`
- Your eventual deployed URL, for example `https://YOUR-DOMAIN/**`

In **Authentication → Providers**, enable Email. Enable Google only after configuring the Google OAuth client ID and client secret in Supabase; add the Supabase callback URL shown by the provider setup to Google Cloud's authorized redirect URIs.

## 3. Run STP

```powershell
npm install
npm run dev
```

Open `http://localhost:3000`.

## Security

- The `sb_publishable_...` key is designed for public client applications. RLS is still essential and is enabled by the supplied schema.
- Never expose `service_role`, `sb_secret_...`, database passwords, or OAuth client secrets in browser code or `VITE_` variables.
- This project currently uses the Supabase browser client for user-scoped database access. Do not add privileged operations to client code.
