---
name: component-creator
description: >-
  A generic workflow for building a design-system-driven component library from
  scratch. Works with any token set or design library. Use when the user wants to
  set up design tokens, create reusable CSS component classes, or build new
  components that stay consistent with their established tokens. Covers three
  phases: token foundation, component library, and component generation.
---

# Design System Component Creator

A universal skill for turning any set of design tokens into a consistent,
reusable component library. Not tied to any specific framework or design
system — works with React, Vue, Svelte, plain HTML, or anything else.

---

## Phase 1 — Build the Token Foundation

> **Goal:** Produce a single `tokens.css` file that holds every design decision
> as a CSS custom property. This file is the source of truth for all visual
> consistency going forward.

### How to Collect Tokens

Ask the user to provide their tokens in whatever form they have:

- Paste from Figma / design tool export
- Copy from an existing style guide or brand doc
- Describe verbally ("our primary blue is #2563EB, spacing uses an 8px grid")
- Reference an existing CSS / SCSS / JSON token file

If the user has **nothing yet**, help them define a minimal viable set by asking
targeted questions. Walk through each category below, one at a time:

**1. Colors** — "What are your brand colors? (primary, secondary, accent)"

```
Collect:
- Primary color + lighter/darker variants
- Secondary / accent colors
- Neutral scale (backgrounds, surfaces, borders, text shades)
- Semantic colors: success, warning, error, info
- Any transparency variants needed
```

**2. Typography** — "What fonts and sizes do you use?"

```
Collect:
- Font families (heading, body, mono)
- Size scale (e.g., 12, 14, 16, 20, 24, 32, 40px)
- Weight scale (normal, medium, semibold, bold)
- Line heights (tight, normal, relaxed)
```

**3. Spacing** — "Do you use a spacing grid? (4px, 8px, etc.)"

```
Collect:
- Base unit (typically 4px or 8px)
- Named scale (xs through 3xl, or numbered)
```

**4. Border Radius** — "How rounded are your elements?"

```
Collect:
- Scale from sharp to fully round (e.g., 4, 8, 12, 16, 9999px)
```

**5. Shadows & Effects** — "Any box shadows or elevation levels?"

```
Collect:
- Elevation levels (subtle, medium, large)
- Any blur or glow effects
```

### Generate `tokens.css`

Once collected, organize everything into a clean `tokens.css` file using this
structure. Use clear, semantic naming so any team member can understand intent:

```css
/* tokens.css — Single source of truth for all design decisions */
:root {
  /* ========================
     COLORS — Brand
     ======================== */
  --color-primary:          #2563eb;
  --color-primary-hover:    #1d4ed8;
  --color-primary-light:    #dbeafe;
  --color-secondary:        #7c3aed;

  /* COLORS — Neutral */
  --color-bg:               #0f1117;
  --color-surface:          #1a1d27;
  --color-surface-hover:    #22262f;
  --color-border:           #2e3340;
  --color-text:             #e4e7ed;
  --color-text-secondary:   #8b90a0;
  --color-text-muted:       #555a6e;

  /* COLORS — Semantic */
  --color-success:          #22c55e;
  --color-warning:          #eab308;
  --color-error:            #ef4444;
  --color-info:             #3b82f6;

  /* ========================
     TYPOGRAPHY
     ======================== */
  --font-family-base:       -apple-system, BlinkMacSystemFont, 'Inter', sans-serif;
  --font-family-heading:    var(--font-family-base);
  --font-family-mono:       'SF Mono', 'Fira Code', monospace;

  --font-size-xs:           0.75rem;   /* 12px */
  --font-size-sm:           0.875rem;  /* 14px */
  --font-size-base:         1rem;      /* 16px */
  --font-size-lg:           1.125rem;  /* 18px */
  --font-size-xl:           1.25rem;   /* 20px */
  --font-size-2xl:          1.5rem;    /* 24px */
  --font-size-3xl:          2rem;      /* 32px */

  --font-weight-normal:     400;
  --font-weight-medium:     500;
  --font-weight-semibold:   600;
  --font-weight-bold:       700;

  --line-height-tight:      1.25;
  --line-height-normal:     1.5;
  --line-height-relaxed:    1.75;

  /* ========================
     SPACING (4px grid)
     ======================== */
  --space-xs:               0.25rem;  /* 4px */
  --space-sm:               0.5rem;   /* 8px */
  --space-md:               0.75rem;  /* 12px */
  --space-lg:               1rem;     /* 16px */
  --space-xl:               1.5rem;   /* 24px */
  --space-2xl:              2rem;     /* 32px */
  --space-3xl:              3rem;     /* 48px */

  /* ========================
     BORDER RADIUS
     ======================== */
  --radius-sm:              4px;
  --radius-md:              8px;
  --radius-lg:              12px;
  --radius-xl:              16px;
  --radius-full:            9999px;

  /* ========================
     SHADOWS
     ======================== */
  --shadow-sm:              0 1px 3px rgba(0, 0, 0, 0.2);
  --shadow-md:              0 4px 12px rgba(0, 0, 0, 0.25);
  --shadow-lg:              0 8px 30px rgba(0, 0, 0, 0.3);

  /* ========================
     TRANSITIONS
     ======================== */
  --transition-fast:        0.15s ease;
  --transition-normal:      0.25s ease;
}
```

**Rules for `tokens.css`:**
- Only CSS custom property declarations — no selectors, no classes, no component styles
- Group by category with clear comment headers
- Use semantic names that describe *intent*, not appearance (e.g., `--color-primary` not `--color-blue`)
- Include a comment showing the resolved value for quick reference (e.g., `/* 16px */`)
- Replace the example values above with the user's actual values

---

## Phase 2 — Build the Component Library

> **Goal:** Produce a `components.css` file with reusable CSS classes for common
> UI patterns. Every class references tokens from `tokens.css` — never raw values.

### When to Create `components.css`

After `tokens.css` exists, ask the user:
"Would you like me to create base component classes now, or wait until we build
our first component?"

If they want it now, generate a starter `components.css` covering the most
common patterns. If they prefer to wait, create it incrementally as new
components are built.

### Structure of `components.css`

Each component block follows this pattern:

```css
/* components.css — Reusable component classes. All values reference tokens.css. */

/* ========================
   BUTTONS
   ======================== */
.btn {
  display: inline-flex;
  align-items: center;
  gap: var(--space-sm);
  padding: var(--space-sm) var(--space-lg);
  font-size: var(--font-size-sm);
  font-weight: var(--font-weight-semibold);
  border-radius: var(--radius-full);
  border: 1px solid var(--color-border);
  background: var(--color-surface);
  color: var(--color-text);
  cursor: pointer;
  transition: all var(--transition-fast);
}
.btn:hover { background: var(--color-surface-hover); }
.btn-primary {
  background: var(--color-primary);
  border-color: var(--color-primary);
  color: #fff;
}
.btn-primary:hover { background: var(--color-primary-hover); }
.btn-danger {
  background: transparent;
  border-color: var(--color-error);
  color: var(--color-error);
}
.btn-sm { padding: var(--space-xs) var(--space-sm); font-size: var(--font-size-xs); }

/* ========================
   CARDS
   ======================== */
.card {
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: var(--radius-lg);
  padding: var(--space-xl);
}

/* ... continue for each component type ... */
```

### What to Include

Build classes for only the components the project actually needs. Common starters:

| Component   | Classes                              | Purpose                              |
|-------------|--------------------------------------|--------------------------------------|
| Buttons     | `.btn`, `.btn-primary`, `.btn-sm`    | Actions and CTAs                     |
| Cards       | `.card`, `.card-header`              | Content containers                   |
| Badges      | `.badge`, `.badge-success`           | Status indicators                    |
| Forms       | `.input`, `.select`, `.form-group`   | Data entry                           |
| Tables      | `.table`, `.table-row`, `.table-cell`| Data display                         |
| Modals      | `.modal`, `.modal-header`            | Dialogs and overlays                 |
| Toggles     | `.toggle`, `.toggle-on`              | Boolean switches                     |
| Avatars     | `.avatar`, `.avatar-sm`              | User representations                 |
| Alerts      | `.alert`, `.alert-error`             | Feedback messages                    |

**Rules for `components.css`:**
- Every value MUST reference a `tokens.css` variable — no raw hex, px, or named colors
- Group by component type with clear comment headers
- Include hover / focus / disabled / active states for interactive elements
- Keep classes flat and composable (`.btn.btn-primary`, not `.btn > .btn-primary`)
- Add new component classes here as the project grows — this file is the living library

---

## Phase 3 — Generate New Components

> **Goal:** When the user asks for a new component, build it using the
> established token and component foundation. Every visual decision maps back to
> an existing token or class.

### Before Writing Any Code

1. **Read `tokens.css`** — confirm the exact variable names available
2. **Read `components.css`** — check what reusable classes already exist
3. **Scan existing components** — reuse before rebuilding

### Step 1 — Analyze the Request

From the user's description, screenshot, Figma link, or wireframe, identify:

- Layout structure (card, list, form, table, page section, modal, etc.)
- Data being displayed and its shape
- Interactive states needed (hover, active, disabled, loading, empty, error)
- Whether existing component classes cover parts of this

### Step 2 — Map Every Decision to a Token

Before writing a single line of code, create a mapping. For example:

```
Container      → .card (from components.css)
Title          → font-size: var(--font-size-xl), font-weight: var(--font-weight-bold)
Body text      → color: var(--color-text-secondary), font-size: var(--font-size-sm)
Spacing        → padding: var(--space-xl), gap: var(--space-md)
Action button  → .btn.btn-primary (from components.css)
Status dot     → color: var(--color-success) | var(--color-error)
```

If a token doesn't exist for what you need, tell the user: "I need a token for
[X]. Should I add `--token-name: value` to `tokens.css`?" Never silently
hardcode a raw value.

### Step 3 — Write the Component

Use whatever framework the project uses. The key constraint is that all styling
flows through the token and component system:

**DO:**
- Use CSS classes from `components.css` as primary styling (`className="card"`)
- Use CSS variables for any inline dynamic styles (`style={{ color: 'var(--color-primary)' }}`)
- Use semantic HTML (`<button>`, `<table>`, `<nav>`, `<section>`, `<article>`)
- Add accessibility attributes: `aria-label` on icon-only buttons, `role` where needed
- Import and reuse existing shared components when they exist
- Use `color-mix(in srgb, var(--token) 50%, transparent)` for transparency variants

**DO NOT:**
- Hardcode hex colors, rgb/rgba values, or named CSS colors
- Invent new CSS variables without adding them to `tokens.css` first
- Use arbitrary pixel values for spacing — use the spacing token scale
- Duplicate styles that already exist in `components.css` — reuse the class
- Create separate CSS files per component — add shared classes to `components.css`

### Step 4 — Add to Component Library (if reusable)

If the new component introduces reusable patterns (e.g., a new card variant, a
stat display, a status badge style), extract the generic CSS into `components.css`
so future components can reuse it.

### Step 5 — Self-Check

Before outputting, verify:

- [ ] Zero hardcoded colors — every color references a `--color-*` token
- [ ] Zero arbitrary spacing — every gap/padding/margin uses a `--space-*` token
- [ ] Font sizes use `--font-size-*` tokens
- [ ] Border radius uses `--radius-*` tokens
- [ ] Interactive elements have hover, focus, and disabled states
- [ ] Existing component classes are reused where applicable
- [ ] Accessibility: icon-only buttons have labels, semantic HTML is used
- [ ] Any new reusable CSS has been added to `components.css`

---

## Quick Reference — File Roles

| File              | Contains                              | Rules                                    |
|-------------------|---------------------------------------|------------------------------------------|
| `tokens.css`      | CSS custom properties only            | No classes. No component styles. Values only. |
| `components.css`  | Reusable CSS component classes        | Every value must reference a token. No raw values. |
| Components        | Application-specific UI code          | Uses classes from `components.css` + tokens from `tokens.css`. |

---

## Example Interaction

**User:** "I want to set up my design tokens. Here are my brand colors:
primary #6366F1, secondary #EC4899, dark bg #0F172A, light text #E2E8F0."

**Agent action:** Ask follow-up questions for typography, spacing, and radius
preferences, then generate `tokens.css` with all values organized by category.

**User:** "Now build me a user profile card with avatar, name, role badge, and
an edit button."

**Agent action:**
1. Read `tokens.css` to confirm available variables
2. Read `components.css` to check for existing `.card`, `.btn`, `.badge`, `.avatar` classes
3. Map every visual decision to a token
4. Build the component using only token references and existing classes
5. If `.avatar` or `.badge` classes don't exist yet, add them to `components.css` first
6. Output the component code
