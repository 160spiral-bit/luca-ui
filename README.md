# Luca — chat UI

React + Vite + TypeScript multi-page app (`index.html` → landing/auth, `chat.html` → chat, `about.html` → about) with Barba.js page transitions.

## Layout

- `src/main.tsx` — boots a React root per Barba container, with a MutationObserver fallback so transitions never strand a blank page.
- `src/App.tsx` — all state: sessions, settings, appearance mode, profile, auth, panels.
- `src/components/` — `Sidebar`, `ChatArea` (thread, status indicator, citations, sources, follow-up chips), `Composer` (input pill, attachments, voice), `Markdown` (lazy-loaded: tables, math, charts, diagrams, code blocks), `Panels` (Settings/Profile/Admin), `Auth` (split-screen sign in/up/verify/forgot/reset), `Logo` (brand spark).
- `src/lib/store.ts` — types + localStorage keys (`luca-*`). `src/lib/api.ts` — streaming client for the chat endpoint.
- `src/barba.ts` — Barba + GSAP transitions. `src/index.css` — all styling (dark + light themes).

## Backend contract

`POST /api/chat` with `{ modelTier, messages, stream, tools, userSettings }` returns SSE `data:` lines (`content`, `reasoning`, `stage`+`label`, `sources`, `searchInfo`, `tool_calls`, `meta`, `[DONE]`). Auth is Bearer JWT (`luca-auth-token`). Per-account sync via `GET/POST /api/user/data`. Follow-ups via `POST /api/followups`.

## Build

`npm run build` → `dist/`.
