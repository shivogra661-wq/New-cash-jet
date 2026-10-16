# CASH JET — connected database demo starter

This ZIP contains the green-theme CASH JET reference UI plus a separate deployable shared-database demo app. It is **not a real-money gambling or payment platform**. Wallet approvals only change demo credits; there is no payment gateway, UPI verification, payout, prizes, or production game settlement.

## Included features
- Player login with IDs created only by Master Admin; no public registration endpoint.
- Master Admin login using a server-side bcrypt password hash.
- Create player ID + temporary PIN, set starting demo balance, disable/enable IDs.
- Player profile update, shared PostgreSQL-backed profile and balance.
- Deposit and withdrawal request queues with approve/reject actions; withdrawal credits are held and returned if rejected.
- Demo play entries with server-side balance checks.
- Master Admin overview with latest five rounds that have bets, round-wise bet totals, entry counts, recent bets and requests.
- PostgreSQL-backed sessions and records; basic rate limiting and request token check.
- `public/green-theme-reference.html` preserves the previously finalized green-theme front end for visual reference. The connected app is `public/index.html`.

## Deploy to GitHub + Railway
1. Unzip this folder and upload the **contents** of `cashjet-working` to a private GitHub repository.
2. In Railway, create a project from that repo and add a PostgreSQL service.
3. Set app Variables: `DATABASE_URL` (Railway Postgres reference), `SESSION_SECRET` (random 32+ character secret), `ADMIN_PASSWORD_HASH` (bcrypt hash), and `NODE_ENV=production`.
4. Create a bcrypt hash locally after `npm install`: `node -e "console.log(require('bcryptjs').hashSync(process.argv[1],12))" "YOUR_LONG_UNIQUE_PASSWORD"`.
5. Set Start Command to `npm start`, generate a public domain, then check `/api/health`.
6. Log in at the site as Master Admin, then use **Create Player ID**. There is no public sign-up.

Never commit `.env`, passwords, PINs or database credentials. Do not treat demo approvals as payments. Before any public production use, obtain appropriate legal/compliance review and independent security testing; implement payment-provider verification, payout controls, account recovery, audit logs, backups, monitoring and any jurisdiction-specific requirements. This starter intentionally does not handle real funds.

## Checks performed in this build
- `node --check server.js` syntax check.
- Static frontend checks for required forms, endpoints, and master-only ID creation flow.
- ZIP integrity check.

A live Railway deployment and real PostgreSQL integration cannot be verified from this local build environment; set variables and deploy before considering it live.
