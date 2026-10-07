# Luxury Tiffins

Production-oriented food delivery starter for **Luxury Tiffins — Ghar Jaisa Khana, Budget Mein**.

## Stack
- Next.js 15 + React 19 + TypeScript
- PostgreSQL + Prisma 6
- Secure JWT session in HttpOnly cookie
- bcrypt password hashing
- Razorpay + Cash on Delivery
- Server-side pincode, price, delivery and coupon validation

## Business rules
- Initial service area: **110096 / New Ashok Nagar, Delhi**
- Free delivery: **orders >= ₹109**
- Delivery below ₹109: **₹15**
- Lunch: 13:00–15:00 IST
- Dinner: 19:00–22:00 IST

## Local setup
1. Install Node.js 20+.
2. Copy `.env.example` to `.env`.
3. Create a PostgreSQL database and set `DATABASE_URL`.
4. Run:

```bash
npm install
npx prisma generate
npx prisma migrate deploy
npm run db:seed
npm run build
npm run start
```

For first-time schema creation in a fresh development database, use `npx prisma migrate dev --name init` instead of `prisma migrate deploy`.

## Environment variables
```env
DATABASE_URL="postgresql://..."
NEXT_PUBLIC_APP_URL="http://localhost:3000"
AUTH_SECRET="replace-with-a-long-random-secret"
RAZORPAY_KEY_ID=""
RAZORPAY_KEY_SECRET=""
ADMIN_EMAIL="admin@luxurytiffins.in"
ADMIN_PASSWORD="ChangeMe123!"
```

Never commit `.env` or expose `RAZORPAY_KEY_SECRET` to the browser.

## Seeded admin
The seed creates the admin using `ADMIN_EMAIL` and `ADMIN_PASSWORD`. Change these values before production seeding.

## Vercel
Create a Vercel project from this repository, add the same environment variables in **Settings → Environment Variables**, and deploy. Make sure the production PostgreSQL database is reachable from Vercel. Run Prisma migrations against the production database before/with deployment.

Recommended build command:
```bash
npm run build
```

Start command:
```bash
npm run start
```

## Important production checklist
- Use a strong random `AUTH_SECRET`.
- Use a managed PostgreSQL provider suitable for Vercel/serverless workloads.
- Configure Razorpay production keys only in server environment variables.
- Add a real image storage/CDN for uploaded food images if required.
- Add a rate-limit provider at the edge/API layer before public launch.
- Test Razorpay webhooks/reconciliation with your merchant account before accepting live payments.
