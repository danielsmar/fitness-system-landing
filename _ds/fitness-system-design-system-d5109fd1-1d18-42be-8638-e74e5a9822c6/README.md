# Fitness System — Design System

**Fitness System** is a dark-first web platform for fitness & health professionals (personal trainers, nutritionists, physiotherapists, physicians) who assess and prescribe training/nutrition programmes for their clients. The SaaS lets professionals manage assistants, clients, schedules, physical assessments (anthropometry, PARQ+, dynamometry, VO₂, cardiac exam, posture, etc.) and exercise prescriptions, with shareable public reports.

Primary language of the product is **Brazilian Portuguese**. The tone is quietly confident, professional, and practical — not "hype-y," not clinical-cold.

---

## Sources consulted

This design system was synthesised from:

1. **Figma file** — *Fitness System | Design UI* (3 pages)
   - `/Fitness-System-Web` — auth flows, dashboards, assessments, prescriptions
   - `/Guia-de-Estllo` — official style guide (colors, type, components)
   - `/Banner` — brand covers
2. **Codebase** — [`fitnessystem/fitness-web`](https://github.com/fitnessystem/fitness-web) (Next.js 16, React 19, Tailwind v4, shadcn/ui, Prisma, lucide-react). Canonical tokens live in `src/app/globals.css`.
3. **Brand uploads** — 8 official logo SVGs (4 horizontal, 4 vertical variants)

None of these require access to open/read this design system — tokens, assets, and guidance have been copied in.

---

## Products represented

- **Fitness System Web** — the professional-facing SaaS (authenticated): dashboard, client management, assessments, prescription builder, schedule, exercise library, profile. (Private routes under `app/(private)`.)
- **Public surfaces** — login, password recovery, public shareable reports (assessments, prescriptions) under `app/(public)`.
- **Brand marks & covers** — 8 logo lockups + a landing banner.

There is a single client-facing product today; *Usuário* (client) login exists in the auth page but their mobile surface is not in the Figma ("A princípio não estará no app" is written on the Cadastro frame).

---

## CONTENT FUNDAMENTALS

**Language.** Brazilian Portuguese. All UI copy, labels, helper text, and error messages are in pt-BR. When adding English-only placeholders (e.g. `Placeholder`, `Helper Text`, `Label`) during design exploration, swap them to Portuguese for final mocks.

**Tone.** Professional, concise, warm. Addresses the user with the polite-informal infinitive where possible:
- *"Entrar como"*, *"Assine agora"*, *"Esqueceu sua senha?"*, *"Enviamos um link para o seu email cadastrado."*
- *"Garanta a segurança da sua conta. Evite senhas simples e não compartilhe com outras pessoas."*

No "you" vs "thou" stance choice is strict — the product mixes *você* (implicit) with imperatives ("Entrar", "Criar nova senha") and descriptive imperatives ("Informa uma nova senha / confirma / ao continuar, volta para a tela de login"). Prefer imperatives on buttons; descriptive sentences in helper text.

**Casing.**
- Buttons → Sentence case, typically single verb or verb + object: *Entrar*, *Criar nova senha*, *Assine agora*.
- Headings → Sentence case with the first word capitalised: *"Entrar como"*, *"Style Guide"*, *"Componentes"*.
- Eyebrow labels in the style guide use full UPPERCASE: *STATE*, *BASE*, *MAIN* (cyan-200 accent).
- Status chips in Portuguese: *Ativo*, *Inativo*, *Sim*, *Não*, *Aberto*, *Fechado*, *Selecionado*, *Pressed*, *Hover* (these are Figma state names — in UI they read as their Portuguese labels).

**No emoji in product copy.** Emoji only appears in the Figma as internal workflow markers ("Liberadas 🟢") — never in production UI. Same goes for unicode-character iconography: not used.

**Fitness-domain vocabulary (keep spelling exact):**
- Avaliações (assessments) · Prescrições (prescriptions) · Antropometria · Anamnese · Exames Clínicos · Perimetria · Diâmetros · Dinamometria · Cardiorrespiratório · Posturologia · PAR-Q+ · VO₂ · Treino · Clientes · Aluno · Profissional · Agendamentos.
- "Fitness System" → two words, both capitalised.

**Microcopy examples:**
- Helper under sent-email form: *"Enviamos um link para o seu email cadastrado."*
- New-password helper: *"Garanta a segurança da sua conta. Evite senhas simples e não compartilhe com outras pessoas."*
- Auth CTA chain: *"Ainda não tem uma conta?"* + *"Assine agora"* (cyan link).
- Forgot link: *"Esqueceu sua senha?"* (right-aligned, cyan, underline on hover).

---

## VISUAL FOUNDATIONS

**Colors.** The palette is built around a single brand cyan/teal (`#3eb1a7`, logomark) with a full 100→800 scale in cyan, plus gray, dark, danger, success, warning, and supporting blue/amethyst/orange scales. The product is **dark-first**; light theme exists but is secondary. See `colors_and_type.css` for canonical `oklch()` values.

- **Brand/primary surface action** — `cyan-500` (#03a6a6) on dark; `cyan-600` on light.
- **Logomark color** — `#3eb1a7` (brand-primary), slightly different from the UI cyan-500 — it is **never** substituted for cyan.
- **Neutrals** — Dark theme backgrounds ladder from `#141414 → #313131`; text ladders `gray-200 → gray-500 → gray-600 → gray-800`.
- **State colors** — success = emerald teal (`#1ad598`), danger = tomato red (`#ea3a3d`), warning = amber (`#f9b959`). Each has a full 100–800 scale.

**Type.** **Outfit** is the one and only UI face, used in weights 300 Light · 400 Regular · 500 Medium · 600 SemiBold · 700 Bold. Base body size is 16px, label 14px, caption 12px. Display headings go 24→30→36→40. Inter is used inside generated PDF reports for a neutral, denser grid; Poppins appears only once (legacy auth sub-line) — **do not introduce Poppins in new work**.

**Backgrounds.** Dark flat fills, never patterned. Two hero treatments:
1. Vertical two-stop gradient `#222222 → #181818` on the brand cover/banner.
2. Login: full-bleed **photograph** (dark-toned gym/running imagery, warm-cool mixed, slight vignette) occupying 60–67% of the viewport on xl screens, paired with a blurred-glass auth panel floating on the right.

No hand-drawn illustrations outside the "empty state" SVG in `src/assets/illustrations/`. No repeating textures, no marble, no grids.

**Animations.** Restrained. Keyframes defined in codebase: `fade-in` (20px up, 0.6s ease-out), `slide-in-left/right` (20px, 0.6s), `scale-in` (0.9→1, 0.5s), `float` (3s), `glow-pulse` (cyan halo, 2s), `gradient-shift` (3s), accordion/collapsible (200ms). No bounces. No springs outside Framer Motion defaults. Standard easing is `ease-out` for enter, `ease` for state change.

**Hover states.** Buttons darken on hover (`bg-button/80` = 80% alpha of the base). Outline/ghost buttons gain a neutral fill (`--button-outline-hover` = `gray-200` light / `gray-800` dark). Links swap from cyan-700 → cyan-600 (light) or cyan-500 → cyan-400 (dark) and gain underline. Cards do **not** lift on hover.

**Press / active states.** No shrink. No scale. Active inputs just tighten the border to `cyan-500` with an inner shadow `inset 0 16px 32px -8px rgba(12,12,13,0.4)` — this is the signature "pressed" feel inside the dark theme.

**Borders.** 1px solid is the default — `gray-200` (light) / `gray-800` (dark) for inputs, `dark-100` for stroke. Focused inputs use `cyan-500`. Dashed borders (`1px dashed #10fafa` / cyan-100) are used in the **style guide only** to frame component groups — *do not* ship dashed borders in the product.

**Shadows.** Two systems:
- **Standard elevation** (cards, popovers): `shadow-xs`/`shadow-sm` using `rgba(16,24,40,0.03)` + `rgba(16,24,40,0.08)` layered.
- **Input inset** (focused/pressed): `inset 0 16px 32px -8px rgba(12,12,13,0.4)` — gives inputs the "sunken" look against the dark surface.
- **Signature glow** (cyan): `glow-pulse` keyframe for celebratory elements only — not a default.

No capsule-only protection gradients; dark surfaces stack on dark backgrounds via raised elevations rather than gradients.

**Corner radii.**
- `6px` — tiny chips
- `8–10px` — swatches, small stickers
- `12px` — **buttons and inputs** (signature)
- `16px` — cards and dialog panels
- `18px` — hero auth panel
- `24px` — style-guide section panels
- `9999px` (full) — avatars, round icon buttons only

**Cards.** Background `dark-300` (#2d2d2d) on dark / `gray-50` on light, 16px radius, 1px `stroke` border, `shadow-sm`. No colored left-border accents. Padding typically 20–24px.

**Transparency & blur.** Used *only* on the auth panel floating over the login photo: `rgba(217,217,217,0.05)` fill + `backdrop-filter: blur(57.504px)` — a heavy frost.  Elsewhere, surfaces are opaque. No scrim gradients over imagery.

**Imagery vibe.** Photography is warm-highlight + cool-shadow, moderate contrast, slight film grain, action-posed (running, lifting). Never monochrome. Avatars are square-cropped with tight portrait framing.

**Layout rules.**
- Fixed **sidebar** left (dark-300) on authenticated routes — collapsible, logo-top, nav groups vertical, avatar bottom.
- Content container maxes at 1536–1920px via named breakpoints: `sm 640 · md 768 · lg 1024 · xl 1280 · 2xl 1536 · full-hd 1920`.
- Input height is **44px** (signature). Button heights: `xs 32 · sm 36 · md 40 · default 44 · lg 52`.
- Grid gap baseline 8, next step 16, hero spacing 24–48.

**Focus rings.** 3px ring at `cyan-500/50` — never removed, never changed color per component.

---

## ICONOGRAPHY

**Primary icon set:** [**Lucide**](https://lucide.dev) (imported as `lucide-react` in the codebase — dep pinned `^1.8.0`). Stroke-based, 2px stroke weight, 24×24 default grid, rounded caps & joints. Use sizes 16 (sm/inline), 20 (default), 24 (nav / headings).

**Fitness-specific icons** that do *not* exist in Lucide are shipped as custom TSX SVG assets in `src/assets/icons/` — they match Lucide's stroke weight:
- `bike-stationary.tsx` · `elliptical.tsx` · `rowing-machine.tsx` · `stairs-machine.tsx` · `walking.tsx`
- `ring-resize-icon.tsx` · `ring-with-bg-icon.tsx` (spinner rings)
- `menu.svg` (hamburger) · `check-circle.svg` (success inline)

All of these are copied into `assets/icons/` in this system.

**Emoji:** **Not used in production UI.** Only appears inside Figma frame/section names as internal workflow markers (e.g. "Liberadas 🟢"). Don't ship emoji.

**Unicode glyph icons (✓, ▾, ×, etc.):** Not used in the product — always the corresponding Lucide icon (Check, ChevronDown, X…) so that size, weight, and color inherit from the same system.

**SVG vs raster:** SVG for every icon and illustration. PNG/WEBP only for photographs (login banners, assessment body-map images) and avatars. Logos are SVG.

**Using icons in designs:**
- Import via Lucide CDN (`https://unpkg.com/lucide@latest`) or `lucide-react` in production.
- Colors should come from semantic tokens — never hard-code a hex on the icon.
- When substituting a missing icon, **flag it** in comments and match stroke weight 2 + rounded caps.

---

## INDEX (file manifest)

Root:
- `README.md` — this file
- `SKILL.md` — Agent Skill entry point
- `colors_and_type.css` — all CSS variables + base type (source of truth)
- `assets/` — logos (horiz + vertical, 4 variants each), brand cover assets, login banners, avatar sample, empty-state illustration, fitness icons
- `assets/icons/` — custom fitness icons lifted from `src/assets/icons`
- `preview/` — Design System tab cards (colors, type, spacing, components, brand)
- `ui_kits/fitness-system-web/` — click-thru React UI kit (Login, Dashboard, Clients, Assessments, Prescriptions)

Supporting:
- `src/` and `public/` — raw imports from `fitnessystem/fitness-web` (kept in-tree so prompts can `read_file` directly into context if they need the source of truth)

### UI kits

- [`ui_kits/fitness-system-web`](ui_kits/fitness-system-web/index.html) — Fitness System web app (professional view). Login → Dashboard → Clients → Assessment viewer → Prescription builder.

---

## CAVEATS

- The uploaded `Outfit.zip` wasn't readable — **Outfit is loaded from Google Fonts** instead. Visually identical; re-upload the `.ttf` if you need self-hosted.
- Poppins appears in one legacy line of the Figma auth flow only; this system intentionally drops it.
- The "Cadastro" (sign-up) page in Figma is flagged *"A princípio não estará no app"* — not yet shipped. It is therefore not included in the UI kit.
- No full mobile app screens were available in Figma; only web surfaces are represented.
