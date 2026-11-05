# بن خلدون — القائمة

Arabic-first café menu and table-ordering app with a staff menu manager, powered by Supabase.

## Run & Operate

- The `artifacts/ibn-khaldoun-menu: web` workflow runs the customer menu.
- `pnpm --filter @workspace/ibn-khaldoun-menu run typecheck` — check the menu app.
- `pnpm run typecheck` — check all workspace packages.
- Add `VITE_SUPABASE_URL` and `VITE_SUPABASE_ANON_KEY` as environment variables, then restart the web workflow.
- Run `artifacts/ibn-khaldoun-menu/supabase/schema.sql` in the Supabase SQL Editor.
- Follow `artifacts/ibn-khaldoun-menu/README.md` to create and allowlist a staff user.

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- Web: React + Vite
- Data and authentication: Supabase Auth, Postgres, and Storage

## Where things live

- `artifacts/ibn-khaldoun-menu/src/App.tsx` — customer menu, cart, table ordering, and `/admin` route.
- `artifacts/ibn-khaldoun-menu/src/pages/AdminPanel.tsx` — staff sign-in and menu editor.
- `artifacts/ibn-khaldoun-menu/src/lib/` — Supabase client, customer orders, and admin operations.
- `artifacts/ibn-khaldoun-menu/supabase/schema.sql` — tables, RLS policies, functions, storage bucket, and starter menu.
- `artifacts/ibn-khaldoun-menu/README.md` — Supabase setup and operating instructions.

## Architecture decisions

- The browser uses only the Supabase public anon key. Never expose a `service_role` key in browser code or in a `VITE_` variable.
- Supabase RLS and database functions restrict staff actions to users in `public.admin_users`.
- The app connects directly to Supabase; the API server and Replit `DATABASE_URL` are not required for this product.

## Product

- Customers browse the Arabic menu, customize items, and submit orders for a table.
- Staff sign in at `/admin` to manage menu items, variants, and ingredient options.
- Submitted orders are saved in Supabase and can be reviewed in its dashboard; an in-app order-management screen is not included.

## User preferences

- The user will add Supabase credentials manually as environment variables.
- Do not add a separate preview feature.

## Gotchas

- Vite reads `VITE_` variables at startup/build time. Restart the web workflow after setting or changing them.
- The SQL setup seeds sample dishes and prices; replace them with the café's real menu before accepting live orders.
- QR links may include `?table=12`; without a table number, customers are prompted to enter one.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
