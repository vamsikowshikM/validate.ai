# VALIDATE.AI 🚀

A visually stunning, single-page web app MVP that accepts a short startup idea and returns a brutally honest, 3-point critique in the voice of a Silicon Valley investor. 

Built in less than 15 Days for the **VALIDATE.AI MVP Builder** project.

## 🎯 What I Built (Summary for Stakeholders)
We successfully built and delivered the **VALIDATE.AI** MVP. 
- **The Product:** Users can submit their startup ideas and select an AI persona (Investor, Architect, Futurist) to receive a brutally honest, 3-point evaluation of their pitch.
- **The Tech:** A sleek, dark-themed Next.js App Router application leveraging Tailwind CSS and Framer Motion for a premium Silicon Valley aesthetic.
- **The Brains:** Google Gemini 1.5 Flash via Serverless Edge functions. All output is strictly JSON-schema validated with automatic exponential backoff retries.
- **The Data:** Real-time polling and persistent storage using a Supabase PostgreSQL database. Identical queries are automatically cached for 1 hour to save API costs.
- **The Scale:** Deployed for high-velocity. Rate limiting is active, and analytics are accessible via the `/analytics` dashboard to track conversions and failures.

## 🌐 Live Demo & Deployment
- **Frontend/Backend:** Configured for Vercel Serverless (using `waitUntil` background processing) or Netlify.
- **Continuous Integration:** Automated GitHub Actions pipeline (`.github/workflows/ci.yml`) is set up to lint and build on every push to `main`.
- **Database:** Supabase PostgreSQL.

### One-Click Deploy
1. Push this repository to GitHub.
2. Visit [Vercel](https://vercel.com/new) and import the repository.
3. Configure the **Environment Variables** (see below).
4. Click **Deploy**.

## 🛠️ Local Development

### 1. Prerequisites
- Node.js 18+
- A [Supabase](https://supabase.com/) account (or local Docker setup).
- A [Google Gemini API Key](https://aistudio.google.com/).

### 2. Environment Variables
Copy `.env.example` to `.env.local` and fill in the values:
```env
GEMINI_API_KEY="your-gemini-key"
NEXT_PUBLIC_SUPABASE_URL="https://your-project.supabase.co"
NEXT_PUBLIC_SUPABASE_ANON_KEY="your-anon-key"
```

### 3. Database Setup
```bash
npx supabase link --project-ref your-project-ref
npx supabase db push
```

### 4. Run the Server
```bash
npm install
npm run dev
```
Open [http://localhost:3000](http://localhost:3000).

---

## 📖 Delivery Artifacts
- **[ROADMAP.md](./ROADMAP.md):** The MVP 15-day timeline and feature tracking.
- **[SYSTEM_PROMPT.md](./SYSTEM_PROMPT.md):** The exact system prompt used for the Gemini LLM.
- **[API_DOCS.md](./API_DOCS.md):** OpenAPI-style markdown documentation for endpoints.
- **[/src/app/analytics](./src/app/analytics/page.tsx):** Simple internal analytics dashboard.

---

## 📘 Runbook & Operations

### Security & Key Rotation
- **LLM API Keys:** If `GEMINI_API_KEY` is compromised, rotate it immediately in Google AI Studio and update the Vercel Environment Variables. The app does not need to be redeployed.
- **Database Keys:** Supabase Row Level Security (RLS) is enabled. Currently, anonymous inserts/selects are permitted for the MVP. In Phase 2, remove the anon policies and implement `supabase.auth` JWT verification.
- **Data Encryption:** All prompts and raw AI outputs are stored in Supabase, which enables transparent data encryption (TDE) at rest by default.

### Scaling & Rate Limits
- **Rate Limiting:** Enforced via `src/lib/rateLimit.ts` (currently in-memory local state, permitting 5 requests per IP per hour). For scale, replace this with Upstash Redis or Vercel KV.
- **Background Jobs:** Vercel `@vercel/functions` `waitUntil()` handles background processing to prevent hitting the 10-second Serverless timeout payload limits.

### Cost Estimates (per 1,000 requests)
- **Vercel Hosting:** Free Tier / $20 Pro (handles easily >10k req/mo).
- **Supabase DB:** Free Tier (handles easily >10k req/mo).
- **Gemini API:** 1,000 requests * ~800 tokens = ~800k processing tokens. **Cost: < $1.00 per month**. 

---
*Built by Antigravity.*
