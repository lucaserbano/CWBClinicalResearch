# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the website for **CWB Clinical Research** — a cardiology clinical research center in Curitiba, Brazil. The site is built with static HTML + Tailwind CSS (CDN). There is no build system, no package.json, and no bundler.

### File Structure

```
/
├── index.html          — Homepage (hero, missão, números, exames, valores)
├── equipe.html         — Team page
├── area-interna/
│   ├── index.html      — Login page (Supabase Auth)
│   └── dashboard.html  — Internal admin panel (patient volunteers list)
└── assets/
    ├── marca/          — Brand assets (logos, pattern, palette)
    └── medicos/        — Doctor photos
```

### Technology Stack

- **HTML** — static, no templating engine
- **Tailwind CSS** — loaded via CDN (`https://cdn.tailwindcss.com?plugins=forms,container-queries`)
- **Fonts** — Manrope (headlines) + Inter (body) via Google Fonts
- **Icons** — Material Symbols Outlined via Google Fonts
- **Supabase** — loaded via CDN (`https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2`) for Auth in `area-interna/`
- **No build tools** — edit HTML files directly

### Design System

- **Primary color**: `#0E385E` (dark navy)
- **Secondary**: `#3B6EA3` (steel blue)
- **Secondary Container**: `#34BDEE` (cyan accent)
- **Primary Container**: `#2F2190` (deep purple)
- **Background/Surface**: `#fcfaf6` (off-white)
- The full Tailwind config is embedded in a `<script id="tailwind-config">` block in each HTML file — keep them in sync when adding new pages.

---

## Área Interna (Internal Area)

The `area-interna/` folder holds the restricted staff-only panel.

### Authentication

- Uses **Supabase Auth** (email + password)
- Admin users must be created manually in the Supabase dashboard under **Authentication → Users**
- The anon key is safe to expose in frontend HTML — access control is enforced via Supabase Row Level Security (RLS)

### Configuring Supabase credentials

Both `area-interna/index.html` and `area-interna/dashboard.html` contain these two constants near the bottom `<script>` block. Replace the placeholder strings:

```js
const SUPABASE_URL      = 'https://bopaymmsxkvkgjoeqilf.supabase.co'
const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...'  // ver arquivos
```

### Future: patient data table

When the `voluntarie-se` page is built, a table (e.g. `voluntarios`) will be created in Supabase to receive form submissions. The dashboard is already structured to display this data — populate `dashboard.html` once the table schema is defined.

---

## Asset Naming Convention

Logo files follow the pattern: `Logo-[orientation]-[style]-[color].png`

- **Orientation**: `horizontal`, `vertical`, or omitted for standalone
- **Style**: `pb` (preto e branco — black & white), `transparente` (transparent background)
- **Color**: `branca` (white), `preta` (black), `colorida` (full color)

## Asset Groups

| File(s) | Purpose |
|---|---|
| `Logo-principal-horizontal.png`, `Logo-principal-vertical.png` | Primary brand logos |
| `Logo-horizontal-*` | Horizontal layout variants (6 files) |
| `Logo-vertical-*` | Vertical layout variants (6 files) |
| `Logo-transparente-*` | Standalone transparent-background logos |
| `Tipografia-e-paleta.png` | Typography and color palette reference |
| `Pattern-principal.png` | Brand pattern/texture |
