---
name: Tailwind Patterns
description: "Use when building UIs with Tailwind CSS. Covers utility-first approach, design tokens, responsive patterns, custom themes, plugin system, and component extraction."
---

# Tailwind Patterns

Tailwind is utility-first: compose small, single-purpose classes instead of writing custom CSS. The constraint is the design system -- stay within the scale and your UI stays consistent.

## Utility-First Approach

- **Compose in markup.** `className="flex items-center gap-4 rounded-lg bg-white p-6 shadow-md"` replaces a custom `.card` class.
- **Avoid premature abstraction.** Repeat utility strings across similar elements before extracting a component. Duplication in markup is cheaper than wrong abstractions in CSS.
- **Use `@apply` sparingly** -- only in base styles or third-party component overrides. If you are writing `@apply` extensively, you are fighting the framework.

## Design Tokens & Theme

- **`tailwind.config.ts`** is your design system. Define colors, spacing, fonts, and breakpoints here -- not in CSS variables.
  ```typescript
  theme: {
    extend: {
      colors: { brand: { 50: '#eff6ff', 500: '#3b82f6', 900: '#1e3a5f' } },
      fontFamily: { sans: ['Inter', ...defaultTheme.fontFamily.sans] },
    },
  }
  ```
- **Extend, don't override.** Use `theme.extend` to add values while keeping Tailwind defaults.
- **Semantic color names** (`brand`, `surface`, `muted`) over raw values (`blue-500`) for maintainability.

## Responsive Patterns

- **Mobile-first.** Unprefixed utilities apply to all sizes; `md:`, `lg:` add overrides at larger breakpoints.
- **Common pattern:** `className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6"`.
- **Container queries** (v3.2+): `@container` and `@lg:` for component-level responsiveness independent of viewport.

## Component Extraction

- **Extract to React/Vue/Svelte components** -- not CSS classes. The component is the abstraction boundary.
  ```tsx
  function Button({ variant = 'primary', children }) {
    const styles = { primary: 'bg-brand-500 text-white', secondary: 'bg-gray-100 text-gray-900' };
    return <button className={`rounded-lg px-4 py-2 font-medium ${styles[variant]}`}>{children}</button>;
  }
  ```
- **`clsx` or `tailwind-merge`** for conditional class composition without conflicts.
- **`cva` (class-variance-authority)** for type-safe variant APIs across multiple props.

## Plugin System

- **Official plugins:** `@tailwindcss/typography` (prose styling), `@tailwindcss/forms` (form resets), `@tailwindcss/container-queries`.
- **Custom plugins** for project-specific utilities:
  ```typescript
  plugin(({ addUtilities }) => {
    addUtilities({ '.text-balance': { 'text-wrap': 'balance' } });
  })
  ```

## Dark Mode

- **`class` strategy** (default in v3.4+): toggle via `.dark` class on `<html>`.
- **Pattern:** `className="bg-white dark:bg-gray-900 text-gray-900 dark:text-gray-100"`.

## Common Pitfalls

| Pitfall | Fix |
|---|---|
| Overusing `@apply` creating a shadow CSS system | Compose utilities in markup; extract components instead |
| String interpolation breaking PurgeCSS | Use complete class names (`bg-red-500`), never `bg-${color}-500` |
| Overriding theme instead of extending | Use `theme.extend` to keep default scale available |
| Conflicting utilities (`p-4 p-6`) | Use `tailwind-merge` to resolve conflicts automatically |
| Giant className strings without organization | Group by concern: layout, spacing, typography, color, state |

## Attribution
**Original** -- Datatide, MIT licensed.
