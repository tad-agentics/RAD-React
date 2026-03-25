# RAD — Rapid App Development

**Template (source only):** [github.com/tad-agentics/RAD-React](https://github.com/tad-agentics/RAD-React) — for **each app**, create a **new repository**, copy the template files into it, and do **all** work and commits **only** in that app repo. **Do not** commit product code to `RAD-React`; treat it as the upstream template, not your project remote.

**RAD** is a fixed order of steps: you define the product, Figma Make builds a working UI prototype, then Cursor agents wire it to Supabase and ship to Vercel. You approve at each gate.

**Stack:** React Router v7 · Vite · Supabase · Vercel · Tailwind · Figma Make

**Who does what:** You talk to the **Tech Lead** in Cursor. Slash commands run specialist agents (design, backend, frontend, QA, deploy). **Figma Make** owns pixels and mock data; agents **integrate** (real data, auth, RLS)—they don’t invent new UI from scratch.

---

## Before you start (once)

- Accounts: [Supabase](https://supabase.com) (dev + prod projects), [Vercel](https://vercel.com), Figma with Make. Add payment/email providers only if your product needs them.
- Cursor: **Auto-run terminal** and **Auto-apply edits** on; use a strong default model (e.g. latest Sonnet).
- Optional: add Context7 to `~/.cursor/mcp.json` (see `RAD-GUIDE.md`).

---

## RAD process — follow in order

### 1. Create a new repo for this project (not `RAD-React`)

Every product gets its **own** GitHub repository. You start from the template files in **[tad-agentics/RAD-React](https://github.com/tad-agentics/RAD-React)** — you never develop with `origin` pointing at `RAD-React`.

**Recommended**

- **GitHub:** On `RAD-React`, **Use this template** → **Create a new repository** (your app’s name) → clone **that** repo locally. `git remote -v` should show **only** your app repo.

- **CLI:** `gh repo create [app-name] --template tad-agentics/RAD-React --private --clone` — this creates **your** repo and checks it out; push only to that repo.

**If you cloned `RAD-React` itself** (e.g. to copy files): create an **empty** repo for the app on GitHub, then run `git remote remove origin` and `git remote add origin https://github.com/[you]/[app-name].git` before the first push — **do not** push app branches to `tad-agentics/RAD-React`.

**Populate template files into an empty app folder** (only `.git` is fine): run **`/populate-from-rad-react`** in Cursor, or from a shell:

```bash
./scripts/populate-from-rad-react.sh
```

If you do not have the script yet, download and run it from the template repo (after that file exists on `main`):

```bash
curl -fsSL https://raw.githubusercontent.com/tad-agentics/RAD-React/main/scripts/populate-from-rad-react.sh | bash -s -- .
```

Then set `git remote` to **your** app repo and commit — not to `RAD-React`.

Open the **app** folder in Cursor.

### 2. Write two docs (before `/init`)

Put these under `artifacts/docs/`:

| File | Purpose |
|------|---------|
| `northstar-[app].html` | Who it’s for, core loop, features, money, auth, integrations |
| `emotional-design-system.md` or `eds-[app].html` | Voice, look/feel, copy rules (same role; see `/init`) |

`/init` stops if these are missing. See **`RAD-GUIDE.md`** for section-by-section format.

### 3. Initialize the project

In chat:

```
/init
```

Then you: fill `.env.local` (Supabase URL + keys), complete `.cursor/mcp.json` if prompted, add PWA icons and fonts per Tech Lead instructions.

### 4. Plan screens + Make brief

```
/phase2
```

**Gate:** Approve the screen specs and `figma-make-brief.md`.

### 5. Build the app in Figma Make (you)

Use the brief in Make. Export/copy **all** code from Make’s Code tab into `src/make-import/`.

### 6. Tech spec

```
/phase4
```

**Gate:** Approve `tech-spec.md` (schema aligned with Make’s mock shapes).

### 7. Build plan

```
/setup
```

**Gate:** Approve `build-plan.md`.

### 8. Foundation (backend + shared UI + landing + auth)

```
/foundation
```

**Done when:** staging shows landing + auth working end-to-end.

### 9. Features (waves)

```
/feature <feature-name>
```

Run features in dependency order; parallelize only when the build plan says it’s safe. Each feature: backend → frontend → QA.

**Gate:** Approve each QA pass before the next wave.

### 10. Visual audit

```
/visual-audit https://your-staging-url.vercel.app
```

**Gate:** Fix everything marked blocking.

### 11. Pre-handoff

```
/pre-handoff
```

**Gate:** Resolve blocking security/quality items.

### 12. Production

```
/deploy <production-supabase-project-ref>
```

Set any env vars the DevOps agent lists. Smoke-test signup, core loop, payments if applicable.

---

## Command cheat sheet

| When | Command |
|------|---------|
| First run | `/init` |
| After init | `/phase2` → Make → `/phase4` → `/setup` → `/foundation` |
| Building | `/feature <name>` |
| Before ship | `/visual-audit <url>` → `/pre-handoff` → `/deploy <ref>` |
| New empty repo (before `/init`) | `/populate-from-rad-react` |
| Helpful | `/status`, `/session-start`, `/research <topic>` |

**Run locally:** `npm run dev` · `npm run build` · `npm test`

---

## More detail

- **Full workflow and env tables:** [`RAD-GUIDE.md`](./RAD-GUIDE.md)
- **Agents, gates, and rules:** [`AGENTS.md`](./AGENTS.md)

**Ideas:** Make owns the UI; Supabase RLS is the security boundary; ship the whole product in one RAD cycle—big new scope usually means a new cycle, not endless patches.
