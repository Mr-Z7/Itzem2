# Itzem — Online Marketplace

Pakistan's online marketplace built with Express + React + Vite + Tailwind + Shadcn UI + PostgreSQL (Drizzle ORM).

## Architecture

**Frontend** — React + Vite, TanStack Query, Wouter routing, Shadcn UI, Tailwind CSS  
**Backend** — Express.js REST API, express-session with connect-pg-simple  
**Database** — PostgreSQL via Drizzle ORM  
**Auth** — bcryptjs password hashing, session-based admin auth

## Key Files

| File | Purpose |
|------|---------|
| `shared/schema.ts` | Drizzle schema + Zod types (users, products, orders, order_items, settings) |
| `server/index.ts` | Entry point — seeds DB on startup |
| `server/routes.ts` | All REST API routes |
| `server/storage.ts` | Database interface (IStorage + PostgresStorage) |
| `server/auth.ts` | bcrypt helpers + requireAdmin middleware |
| `client/src/App.tsx` | Wouter router — all page registrations |
| `client/src/components/layout.tsx` | Header + footer shared layout |
| `client/src/context/cart-context.tsx` | Cart state (localStorage: `itzem_cart`) |
| `client/src/lib/queryClient.ts` | TanStack Query client + apiRequest helper |

## Pages

### Public
- `/` — Home (hero, categories, best sellers, newsletter)
- `/products` — Product listing with search, filter by category, sort
- `/deals` — Products with discounts (originalPrice > price)
- `/about` — About page with stats, mission, team
- `/contact` — Contact form + social links + support hours
- `/product/:id` — Product detail with quantity picker and related products
- `/cart` — Cart with checkout form (Stripe toggle or COD)
- `/checkout/success` — Order confirmation

### Admin (requires admin session)
- `/admin/login` — Login form (default: admin/admin123)
- `/admin` — Dashboard with stats + recent orders
- `/admin/products` — CRUD product table with modal form
- `/admin/orders` — Order list with status dropdowns
- `/admin/settings` — Social links, contact info, Stripe keys

## Color Palette (Sky Blue Theme)

| Variable | Value | Usage |
|----------|-------|-------|
| Primary | `#38BDF8` | Accent text, hero highlight |
| Action | `#0EA5E9` | Buttons, active states |
| Hover | `#0284C7` | Button hover |
| Light BG | `#E0F2FE` | Page sections, admin bg |
| Dark | `#0F172A` | Headings, nav bg, footer |
| Nav accent | `#0369A1` | Category badges |

## Database Tables

- **users** — id (uuid), username, password (hashed), isAdmin
- **products** — id, name, price, originalPrice, category, description, images[], badge, rating, reviewCount, inStock
- **orders** — id, customerName, customerEmail, customerPhone, customerAddress, totalAmount, status, paymentStatus, stripeSessionId, createdAt
- **order_items** — id, orderId, productId, productName, productPrice, quantity
- **settings** — key, value (social links, contact info, Stripe keys)

## Seed Data

On startup, `server/index.ts` auto-seeds:
- Admin user: `admin` / `admin123`
- 22 products across 6 categories
- Default social/contact/Stripe settings

## Currency

All prices are integers in PKR. Display format: `₨ ` + `toLocaleString("en-PK")`. Never divide by 100.

## Stripe Integration

Admin enters Stripe keys in `/admin/settings`. The backend reads them from the DB at checkout time. Webhook at `/api/webhooks/stripe` marks orders as paid.

## Session

`SESSION_SECRET` env var (falls back to dev string). 7-day cookie. `req.session.userId` + `req.session.isAdmin` set on login. `requireAdmin` middleware protects all `/api/admin/*` routes.
