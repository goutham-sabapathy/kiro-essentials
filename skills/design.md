# Design

Enforces precise, minimal design for dashboards and admin interfaces. Use when building SaaS UIs, data-heavy interfaces, or any product needing high craft.

**Core philosophy:** Every interface should look designed by a team that obsesses over 1-pixel differences. Not stripped, _crafted_.

## Design Direction (REQUIRED)

**Before writing code, commit to a direction.**

### Choose a Personality

| Direction | Feel | When to Use |
|-----------|------|-------------|
| Precision & Density | Tight spacing, monochrome, info-forward | Power users. Linear, Raycast. |
| Warmth & Approachability | Generous spacing, soft shadows | Collaborative tools. Notion, Coda. |
| Sophistication & Trust | Cool tones, layered depth | Finance, sensitive data. Stripe, Mercury. |
| Boldness & Clarity | High contrast, dramatic negative space | Modern dashboards. Vercel. |
| Utility & Function | Muted palette, functional density | Developer tools. GitHub. |
| Data & Analysis | Chart-optimized, technical but accessible | Analytics, BI tools. |

### Choose Foundation

**Color foundation:**
- Warm (creams, warm grays): approachable, human
- Cool (slate, blue-gray): professional, serious
- Pure neutrals (true grays): minimal, technical
- Tinted (slight color cast): distinctive, branded

**Accent color:** ONE that means something. Blue = trust. Green = growth. Orange = energy. Violet = creativity.

### Choose Typography

- **System fonts**: fast, native, invisible
- **Geometric sans** (Geist, Inter): modern, clean
- **Humanist sans** (SF Pro, Satoshi): warmer
- **Monospace influence**: technical, data-heavy

## Core Craft (Non-Negotiable)

### The 4px Grid
All spacing: `4px`, `8px`, `12px`, `16px`, `24px`, `32px`.

### Symmetrical Padding
TLBR must match. If top is 16px, all sides are 16px.

### Border Radius
Stick to 4px grid. Pick a system:
- Sharp: 4px, 6px, 8px
- Soft: 8px, 12px
- Minimal: 2px, 4px, 6px

### Typography Hierarchy
- Headlines: 600 weight, -0.02em tracking
- Body: 400-500 weight
- Labels: 500 weight, positive tracking for uppercase
- Scale: 11px, 12px, 13px, 14px (base), 16px, 18px, 24px, 32px
- Use **monospace** for numbers, IDs, codes, timestamps
- Use `tabular-nums` for columns

### Color for Meaning Only
Gray builds structure. Color only appears when it communicates: status, action, error, success.

## Depth Strategy

- **Borders-only (flat)**: Clean, technical
- **Subtle single shadow**: Soft lift
- **Layered shadows**: Rich, premium
- **Surface color shifts**: Background tints for hierarchy

## Motion & Animation

- **Timing:** 150-200ms micro-interactions, 300-400ms larger transitions
- **Easing:** `ease-out` entrances, `ease-in` exits, `ease-in-out` state changes
- **Staggered reveals:** 50-75ms stagger for multiple items

Avoid: Spring physics, bouncy overshoots, parallax effects.

## Dark Mode

- Borders over shadows (shadows less visible on dark)
- Desaturate semantic colors for dark backgrounds
- Same hierarchy, inverted values

## Anti-Patterns

Never:
- Dramatic drop shadows
- Large radius (16px+) on small elements
- Asymmetric padding without reason
- Pure white cards on colored backgrounds
- Thick borders (2px+) for decoration
- Multiple accent colors
- Motion without purpose

## CSS Quick Reference

```css
/* Shadow system */
--shadow-sm: 0 1px 2px rgba(0,0,0,0.05);
--shadow-md: 0 4px 6px rgba(0,0,0,0.07);
--shadow-lg: 0 10px 15px rgba(0,0,0,0.1);

/* Spacing */
--space-1: 4px;  --space-2: 8px;  --space-3: 12px;
--space-4: 16px; --space-6: 24px; --space-8: 32px;

/* Typography */
--text-xs: 11px; --text-sm: 12px; --text-base: 14px;
--text-lg: 16px; --text-xl: 18px; --text-2xl: 24px;

/* Transitions */
--transition-fast: 150ms ease-out;
--transition-base: 200ms ease-out;
--transition-slow: 300ms ease-in-out;
```
