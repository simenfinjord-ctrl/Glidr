# Deploy Glidr on Render

This is the easiest path for this project and avoids the Vercel issue where "Visit" downloads a file.

## 1) Push this repository to GitHub

Render deploys from GitHub. Make sure your latest code is pushed.

## 2) Create Render services from blueprint

1. Go to [Render Dashboard](https://dashboard.render.com/).
2. Click **New** -> **Blueprint**.
3. Select this repository (`simenfinjord-ctrl/Glidr`).
4. Render will detect `render.yaml` and propose:
   - `glidr-web` (Node web service)
   - `glidr-db` (PostgreSQL database)
5. Click **Apply**.

## 3) Set required environment variables

In `glidr-web` service settings, confirm:

- `NODE_ENV=production` (already set in blueprint)
- `DATABASE_URL` from `glidr-db` (already linked in blueprint)
- `SESSION_SECRET` generated value (already set in blueprint)

Optional if you use AI endpoints:

- `AI_INTEGRATIONS_OPENAI_API_KEY`
- `AI_INTEGRATIONS_OPENAI_BASE_URL`

## 4) First deploy checks

After deploy:

1. Open service logs and verify app started on `PORT`.
2. Open the Render URL (for example `https://glidr-web.onrender.com`).
3. Confirm frontend loads and API responds.

## 5) Connect your custom domain

1. In Render, open `glidr-web` -> **Settings** -> **Custom Domains**.
2. Add your domain (for example `app.yourdomain.com`).
3. Render shows the DNS records to add at your domain registrar:
   - usually one `CNAME` for subdomain, or
   - `A/ALIAS` records for apex/root domain.
4. Wait for DNS propagation, then enable HTTPS (Render handles certificates automatically).

## Notes

- This app includes an Express backend, so Render is a better fit than Vercel for this setup.
- If login/session behaves oddly, verify app is served over HTTPS and `SESSION_SECRET` is set.
