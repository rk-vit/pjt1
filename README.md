# Vercel Incident Endpoint Function

A minimal, production-ready Vercel Serverless Function exposing the REST endpoint `/incident`.

## Project Structure

```text
├── api/
│   └── incident.ts     # Serverless Function handler for /incident
├── .gitignore          # Git ignore rules for node_modules and .vercel
├── package.json        # Dependencies and scripts
├── tsconfig.json       # TypeScript configuration
├── vercel.json         # Rewrites to route /incident -> /api/incident
└── README.md           # Instructions
```

## How It Works

- The entrypoint is located at [`api/incident.ts`](file:///C:/Users/revan/Documents/PJT1/api/incident.ts).
- [`vercel.json`](file:///C:/Users/revan/Documents/PJT1/vercel.json) rewrites incoming requests to `/incident` directly to `/api/incident`.
- Exclusively accepts `POST` requests (and `OPTIONS` for CORS preflight); other methods return `405 Method Not Allowed`.
- Logs timestamp, URL, client IP, headers, query parameters, and incoming payload/body to the Vercel console logs.
- Returns a `200 OK` JSON response acknowledging receipt of the incident request.

## Local Testing

You can run the function locally using the Vercel CLI:

```bash
npx vercel dev
```

Then test it with curl or Postman:

```bash
# Test POST with payload
curl -X POST http://localhost:3000/incident \
  -H "Content-Type: application/json" \
  -d '{"title": "High CPU Usage", "severity": "critical"}'

# Test invalid method (returns 405)
curl http://localhost:3000/incident
```

## Deployment to Vercel

### Option 1: Via Vercel CLI
```bash
npx vercel
```
To deploy directly to production:
```bash
npx vercel --prod
```

### Option 2: Via Git (GitHub / GitLab / Bitbucket)
1. Push this repository to GitHub/GitLab.
2. Import the repository in your [Vercel Dashboard](https://vercel.com/new).
3. Vercel automatically detects the serverless function and deploys it.
