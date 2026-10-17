# CASH JET — Railway deployable demo

**This is a demo-credit app only.** It does not process real payments, UPI transfers, cash-outs, prizes, or real-money gambling.

## Files
- `server.js` and `package.json` are at repository root (important for Railway).
- `public/index.html` is the player interface.
- `public/admin.html` is the separate Master Admin login page.
- `public/green-theme-reference.html` is a design reference only.

## Railway deployment
1. Extract this ZIP and upload the **contents** (not the ZIP file) to the root of your GitHub repository.
2. Railway should use Root Directory `/` and Start Command `npm start` (or leave start command blank; package.json has `start`).
3. Add a Railway PostgreSQL service and set the app variable `DATABASE_URL` to the PostgreSQL service's connection URL/reference.
4. Set `SESSION_SECRET` to a long random value (32+ characters).
5. Set `ADMIN_PASSWORD` to a strong password of your choice. Do not rely on the demo default for a public deployment. If `ADMIN_PASSWORD_HASH` is set, it takes precedence.
6. Set `NODE_ENV=production`.
7. Redeploy. Check `/api/health`; it should return JSON with `ok: true` and `database: "connected"`.
8. Admin page: `/admin`.

If `/api/health` gives 404, the new server code is not the service currently handling the domain; verify the Railway service's source repository, deployment branch, root directory, and latest successful deployment.

## Local checks
- `npm install`
- `npm run check`
- `npm start`

`DATABASE_URL` and `SESSION_SECRET` are required; the server intentionally refuses to start without them. Do not commit `.env` or secrets.
