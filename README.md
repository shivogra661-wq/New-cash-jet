# CASH JET — connected database demo starter

This ZIP has the deployable app files at the ZIP root (no extra nested folder), to avoid Railway Root Directory confusion. It contains the green-theme CASH JET reference UI plus a shared-database demo app. It is **not a real-money gambling or payment platform**. Wallet approvals only change demo credits; there is no payment gateway, UPI verification, payout, prizes, or production game settlement.

## Included features
- Player login with IDs created only by Master Admin; no public registration endpoint.
- Master Admin login using a server-side bcrypt password hash. **Default demo admin password: `Chiku1234`** (unless `ADMIN_PASSWORD_HASH` or `ADMIN_PASSWORD` is set in Railway Variables). Change it before sharing/public use.
- Create player ID + temporary PIN, set starting demo balance, disable/enable IDs.
- Player profile update, shared PostgreSQL-backed profile and balance.
- Deposit and withdrawal request queues with approve/reject actions; withdrawal credits are held and returned if rejected.
- Demo play entries with server-side balance checks.
- Master Admin overview with latest five rounds that have bets, round-wise bet totals, entry counts, recent bets and requests.
- PostgreSQL-backed sessions and records; basic rate limiting and request token check.
- `public/green-theme-reference.html` preserves the previously finalized green-theme front end for visual reference. The connected app is `public/index.html`.

## Deploy to GitHub + Railway
1. Unzip this ZIP and upload the files/folders directly to the root of a private GitHub repository. `package.json` and `server.js` must be visible at the repository root.
2. In Railway, create a project from that repo and add a PostgreSQL service.
3. Set app Variables: `DATABASE_URL` (Railway Postgres reference), `SESSION_SECRET` (random 32+ character secret), and `NODE_ENV=production`. The ZIP has demo fallback password `Chiku1234`; for safer deployment, set `ADMIN_PASSWORD_HASH` to a bcrypt hash of your chosen password (this overrides the fallback).
4. Create a bcrypt hash locally after `npm install`: `node -e "console.log(require('bcryptjs').hashSync(process.argv[1],12))" "YOUR_LONG_UNIQUE_PASSWORD"`.
5. In Railway Settings, set Root Directory to `/` (or leave it blank if Railway treats that as repository root); set Start Command to `npm start`, generate a public domain, then check `/api/health`. The service must be connected to the PostgreSQL service and have `DATABASE_URL`, `SESSION_SECRET` (32+ chars), and `NODE_ENV=production` variables.
6. Log in at the site as Master Admin, then use **Create Player ID**. There is no public sign-up.

Never commit `.env`, passwords, PINs or database credentials. The fallback password is included only for this demo and must be changed before public use. Do not treat demo approvals as payments. Before any public production use, obtain appropriate legal/compliance review and independent security testing; implement payment-provider verification, payout controls, account recovery, audit logs, backups, monitoring and any jurisdiction-specific requirements. This starter intentionally does not handle real funds.

## Checks performed in this build
- `node --check server.js` syntax check.
- Static frontend checks for required forms, endpoints, and master-only ID creation flow.
- ZIP integrity check.

A live Railway deployment and real PostgreSQL integration cannot be verified from this local build environment; set variables and deploy before considering it live.


## Important Railway check
- The app needs a Railway PostgreSQL database. Without a valid `DATABASE_URL`, it intentionally stops instead of pretending to work.
- Set `SESSION_SECRET` to a unique random string of at least 32 characters.
- Admin page: `/admin`. Default demo password is `Chiku1234` only if neither `ADMIN_PASSWORD` nor `ADMIN_PASSWORD_HASH` is configured. Change it before public use.
- Health endpoint: `/api/health`; it returns JSON and verifies the database connection.
