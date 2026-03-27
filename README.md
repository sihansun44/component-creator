# Component Creator — Cursor Skill

A generic [Cursor AI](https://cursor.com) skill for building design-system-driven components from scratch. Works with **any design library, any token set, any framework** — not tied to a specific system.

This skill teaches Cursor a three-phase workflow: collect design tokens, build a reusable component CSS library, and generate new components that stay consistent with your established foundation.

## Available Skills

| Skill | Description |
|-------|-------------|
| [component-creator](./component-creator/SKILL.md) | Builds `tokens.css` from designer input, creates reusable `components.css` classes, and generates new components that strictly reference the token system. |

## Installation

### Option 1: Add to a single project

```bash
# From your project root
mkdir -p .cursor/skills/component-creator

curl -o .cursor/skills/component-creator/SKILL.md \
  https://raw.githubusercontent.com/sihansun44/component-creator/main/component-creator/SKILL.md
```

### Option 2: Clone into your project

```bash
# From your project root
git clone https://github.com/sihansun44/component-creator.git .cursor/skills
```

### Option 3: Install globally (all Cursor projects)

```bash
git clone https://github.com/sihansun44/component-creator.git ~/.cursor/skills/component-creator
```

## How It Works

The skill follows three phases:

### Phase 1 — Token Foundation
Cursor asks the designer to paste or describe their tokens (colors, typography, spacing, radius, shadows). It generates a clean `tokens.css` with only CSS custom properties — the single source of truth.

### Phase 2 — Component Library
Cursor creates `components.css` with reusable CSS classes (buttons, cards, badges, forms, etc.) that strictly reference tokens. No hardcoded values.

### Phase 3 — Component Generation
When building new UI, Cursor reads the token and component files, maps every visual decision to an existing token or class, and outputs consistent code. Any new reusable patterns get added back to `components.css`.

## File Structure

Once set up, your project will have:

| File | Contains | Rules |
|------|----------|-------|
| `tokens.css` | CSS custom properties only | No classes. No component styles. Values only. |
| `components.css` | Reusable CSS component classes | Every value must reference a token. No raw values. |
| Components | Application-specific UI code | Uses classes from `components.css` + tokens from `tokens.css`. |

## What Makes This Different

- **Framework agnostic** — works with React, Vue, Svelte, plain HTML, or anything else
- **Library agnostic** — not tied to any specific design system; bring your own tokens
- **Designer-friendly** — starts from what the designer already has (Figma exports, brand docs, or verbal descriptions)
- **Self-enforcing** — includes a constraint checklist that prevents hardcoded values from slipping through

## License

MIT
