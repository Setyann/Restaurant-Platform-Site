# Restaurant Platform

QR-menu and table ordering for restaurants. Guests scan a QR code on the table, choose dishes and send the order. The order appears on the staff screen at once, and the guest sees its status. No app to install and no sign-up for guests.

**Website:** https://setyann.github.io/Restaurant-Platform-Site/
**Demo menu:** https://setyann.github.io/Restaurant-Platform/?restaurant=demo

## Features

- QR menu for each table, opened in the guest's browser
- Order sent from the table, with the price calculated by the server
- Staff window with statuses: received, preparing, ready, served
- Order status visible to the guest
- Menu in three languages: Armenian, Russian and English
- Owner panel with two-factor authentication: menu, tables, staff, restaurant details, change log
- Row-level security in the database; guests can only read the published menu
- Protection against spam: limits per table, per client and per restaurant, and a unique request id for each order

## Plans

- **Free:** view the QR menu only
- **Standard:** table ordering and the staff window
- **Pro:** planned. Several venues in one account; the details are still being defined

## How it works

1. The owner creates a table in the admin panel and gets its link.
2. The owner turns the link into a QR code with any QR generator and puts it on the table.
3. The guest scans the code, adds dishes and sends the order.
4. The order goes to the staff window. Staff move it forward: accepted, ready, served.
5. The guest sees the current status on the same page.

## Tech stack

- Vite, plain JavaScript
- Supabase (PostgreSQL, Row Level Security, Auth with TOTP)
- GitHub Pages for hosting

## Project structure

```
src/
  main.js               guest menu and ordering
  staff.js              staff window
  admin.js              owner panel
  services/             menu, orders and Supabase client
  utils/                cart, plans, texts, validation
supabase/
  migrations/           database schema, functions and grants
  verify.sql            database checks, run in a test project
tests/                  unit tests
```

## Run locally

```
npm install
npm run dev
```

Create a file `.env.local` in the project root:

```
VITE_SUPABASE_URL=your-project-url
VITE_SUPABASE_PUBLISHABLE_KEY=your-publishable-key
```

Use only the publishable key in the frontend. The service role key must never appear in the code.

## Database setup

Run the files in `supabase/migrations/` in the Supabase SQL Editor, in this order:

1. `001_roles_security_orders.sql`
2. `002_grants.sql`
3. `003_restaurant_info.sql`

Then run `supabase/verify.sql` on a test project. All checks should be `true`.

## Tests

```
npm test
```

## Deploy

The guest menu is published with GitHub Pages. The build needs the two environment variables above, set as repository secrets in GitHub Actions.

## Status

The system has been tested on a test database and in the browser. It has not yet been used in a real restaurant: a pilot is planned.

## Contact

- Telegram: [@Setyann](https://t.me/Setyann)
- GitHub: [Setyann](https://github.com/Setyann)

## License

All rights reserved. The source code is private and is not published.
Use of the system requires a written agreement with the author.