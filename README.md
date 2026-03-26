# Momentum Design System — Cursor Skills

A collection of [Cursor AI](https://cursor.com) skills for building components with the **Momentum Design System** (Webex AI Agent Studio).

These skills teach Cursor how to generate components that follow your design system's tokens, CSS classes, and conventions — so every component it builds is automatically consistent.

## Available Skills

| Skill | Description |
|-------|-------------|
| [component-creator](./component-creator/SKILL.md) | Generates React components using Momentum Design tokens, CSS component classes, and accessibility best practices. |

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
git clone https://github.com/sihansun44/component-creator.git ~/.cursor/skills/momentum
```

## Prerequisites

These skills assume your project has the Momentum Design System CSS files:

| File | Purpose |
|------|---------|
| `src/tokens/*.css` | Raw design tokens (colors, spacing, fonts, radii, effects) |
| `src/tokens.css` | Semantic aliases (`--text-primary`, `--accent-color`, etc.) |
| `src/components.css` | Component CSS classes (`.btn`, `.card`, `.tabs`, `.modal`, etc.) |
| `src/index.css` | Import chain that loads everything in order |

See the [Momentum Testing](https://github.com/webexdesign/Momentum-Testing) repo for a complete reference implementation.

## How It Works

Once installed, Cursor automatically detects the skill. When you ask it to build a component, it will:

1. **Read your tokens and CSS** to find exact class names and variables
2. **Map every visual decision** to existing tokens (no hardcoded colors or spacing)
3. **Reuse shared components** (Button, Card, Badge, etc.) instead of reinventing
4. **Follow accessibility best practices** (semantic HTML, aria labels, focus states)
5. **Self-check** against a constraint checklist before outputting

## License

MIT
