# CLAUDE.md — DealDesk Component Instructions

> This file is the standing instruction set for Claude (chat) and Claude Code. Read it in full before generating any code. Do not deviate from these rules unless explicitly instructed in the prompt.

---

## Project Overview

**Application:** DealDesk — a B2B deal management dashboard for sales teams.  
**Stack:** Next.js 14 (App Router), TypeScript, Tailwind CSS, no additional UI libraries.  
**Audience:** Non-developer product designers using AI-assisted code generation. Output must be immediately runnable without additional setup.

---

## Repository Structure

```
dealdesk-app/
├── app/                        # Next.js App Router pages
│   └── page.tsx
├── components/
│   ├── atoms/                  # Single-purpose, token-styled primitives
│   └── molecules/              # Compositions of atoms
├── docs/
│   ├── CLAUDE.md               # This file
│   ├── DESIGN.md               # Visual brand system (read by Claude Design)
│   ├── design-system.md        # Human-readable token + style reference
│   └── components/             # One .md spec per component
├── tokens/
│   └── tokens.json             # Figma token export — source of truth for all values
└── tailwind.config.ts          # Maps token names to Tailwind utility classes
```

**Rule:** Before generating code for any component, check `/docs/components/` for an existing spec. If one exists, follow it exactly.

---

## Design Tokens

All visual values originate in `tokens/tokens.json` (exported from Figma via Tokens Studio) and are mapped to Tailwind in `tailwind.config.ts`. The current token set for Mode 1 is:

| Token | Value | Tailwind Class |
|---|---|---|
| Surface (card background) | `#FFFFFF` | `bg-surface-card` |
| Stroke (border) | `#BDBDBD` | `border-stroke` |
| Color/Positive | `#4CAF50` | `text-color-positive` |
| Color/Negative | `#F44336` | `text-color-negative` |
| Color/Text/Primary | `#000000` | `text-text-primary` |
| Color/Text/Secondary | `#616161` | `text-text-secondary` |
| Text size / 12 | `12px` | `text-[token-12]` |
| Text size / 24 | `24px` | `text-[token-24]` |
| Spacing / 24 | `24px` | `p-spacing-24` / `gap-spacing-24` |
| Spacing / 32 | `32px` | `p-spacing-32` / `gap-spacing-32` |
| Corner radius / 8 | `8px` | `rounded-radius-8` |

### Token Rules — STRICT

- **NEVER** use arbitrary Tailwind values: no `text-[#4CAF50]`, no `p-[14px]`.
- **NEVER** use raw Tailwind palette classes: no `text-green-500`, no `bg-white`, no `rounded-lg`.
- **NEVER** use inline styles (`style={{}}`).
- **ALWAYS** use the token-mapped classes above. If a needed value isn't in the table, ask before inventing a new class.

---

## Atomic Design Structure

This project follows **Atomic Design** (Brad Frost). Respect the hierarchy strictly.

### Atoms — `/components/atoms/`
Single-responsibility UI primitives. Each atom:
- Renders one element or a trivially simple wrapper
- Accepts only the props it directly needs
- Applies exactly the token classes specified in its spec
- Has no knowledge of layout or sibling components

Existing atoms:
- `Label.tsx` — secondary-colored label text
- `Value.tsx` — large, bold, primary-colored metric value
- `TrendIcon.tsx` — directional glyph (↑ ↓ →) colored by trend
- `ChangeIndicator.tsx` — small trend-colored change text

### Molecules — `/components/molecules/`
Compositions of two or more atoms that form a distinct UI unit.
- Import and compose existing atoms; do not re-implement atom logic inside a molecule.
- Accept props at the molecule level and pass them down to atoms.
- Own their own layout (flexbox, grid, spacing between atoms).

### Rule
Never skip a level. A molecule must be built from atoms. A page imports molecules. If an atom doesn't exist yet, generate it first, then compose the molecule.

---

## TypeScript Rules

- All components use **explicit prop interfaces** (`interface Props { ... }`), defined above the component.
- No `any` types. No implicit `any`.
- Use `React.FC<Props>` or inline return type annotation.
- Union types for constrained values: `trend: "positive" | "negative" | "neutral"`.
- All props that are required must be marked as such (no unnecessary `?` optionals).

---

## Component Authoring Rules

1. **Named exports only.** `export const StatCard = ...` — never `export default`.
2. **JSDoc comment** above every component describing its purpose and props.
3. **Keep components under 100 lines.** If a component exceeds this, decompose it.
4. **No logic in JSX.** Extract conditionals and mappings to variables or helper functions before the return statement.
5. **Accessibility:** All interactive elements must be keyboard accessible. Use semantic HTML. Include `aria-label` where icon-only elements appear.
6. **No hardcoded strings** for UI copy that should be a prop.
7. **Complete files only.** Output the full file — no fragments, no `// ... rest of file` placeholders.

---

## Code Quality Standards

- **Immutability:** Prefer `const`. Never reassign variables unless unavoidable.
- **Pure functions:** Components should be pure — given the same props, they produce the same output.
- **No side effects in render.** Use `useEffect` for side effects; never inside render logic.
- **No dead code.** Do not include commented-out code, unused imports, or unused variables.
- **Consistent naming:**
  - Components: `PascalCase`
  - Props interfaces: `PascalCase` + `Props` suffix (e.g., `StatCardProps`)
  - Utility functions: `camelCase`
  - Files: match the component name exactly (`StatCard.tsx`)

---

## Security

- **No `dangerouslySetInnerHTML`** unless the input is explicitly sanitized and the use is justified in a comment.
- **No `eval()`** or dynamic code execution.
- Props that accept user-generated content should be treated as untrusted — do not render raw HTML from them.
- Do not hardcode credentials, API keys, or environment-specific URLs. Use `process.env` variables.

---

## What to Do When Generating Code

1. Read the component spec in `/docs/components/` for the target component.
2. Check `/components/atoms/` for existing atoms before creating new ones.
3. Apply only token-mapped Tailwind classes (see Token Rules above).
4. Output the **complete file** — interface, JSDoc, component, named export.
5. Verify the output satisfies every item in the **Pre-Commit Checklist** below.

## Pre-Commit Checklist

Before outputting any component, confirm:
- [ ] All colors, spacing, and radii use token-mapped Tailwind classes
- [ ] No arbitrary values, inline styles, or raw palette classes
- [ ] Explicit TypeScript interface defined
- [ ] JSDoc comment present
- [ ] Named export (not default)
- [ ] No component exceeds 100 lines
- [ ] All atoms imported from `/components/atoms/` — no re-implementation
- [ ] Accessible: semantic HTML, keyboard navigable, aria labels where needed
- [ ] File is complete — no placeholders or fragments

---

## Reference Files

| File | Purpose |
|---|---|
| `tokens/tokens.json` | All design token values — consult before adding any visual value |
| `docs/DESIGN.md` | Visual brand system — read by Claude Design, reference for visual intent |
| `tailwind.config.ts` | Token-to-class mappings — must stay in sync with `tokens.json` |
| `docs/components/*.md` | Per-component specs — authoritative source for props, anatomy, token usage |

---

*DealDesk MVP Program · CLAUDE.md v1.0*