# Zevio AI — Standalone Project

This folder contains the Zevio AI application extracted from the uploaded KhmerSRT website archive.

## Included
- `frontend/` — React + TypeScript + Vite user interface, source code, and the existing production build in `frontend/dist/`.
- `backend/` — Node.js + Express + TypeScript API source and build output.
- `database/` — Supabase SQL schema.
- `gpu-server/` — vLLM GPU deployment examples and setup notes.

## Excluded for safety and size
- `backend/.env` — environment files can contain private credentials. Create your own local `.env` from `.env.example`.
- `node_modules/` — dependencies should be installed with `npm install`.
- Wrangler local state and caches.

## Important setup notes
1. Review `backend/.env.example` and configure your own backend environment variables.
2. Do not publish API keys, service-role keys, passwords, or private tokens in GitHub.
3. Install backend dependencies inside `backend/`, then run `npm run build` and `npm start`.
4. Install frontend dependencies inside `frontend/`, then run `npm run build`.
5. The app's AI providers and inference services need valid configuration and reachable services. Extracting the project does not provision or activate a hosted AI model, GPU server, Supabase project, or API subscription.

## Quick local development
Backend:
```bash
cd backend
npm install
npm run dev
```

Frontend (in another terminal):
```bash
cd frontend
npm install
npm run dev
```

See the original `README.md` and `gpu-server/README-GPU-SETUP.md` for the project's own architecture and GPU deployment notes.
