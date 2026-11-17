---
name: uiux-development
description: >-
  Hallmark UI/UX design system and workflow for the Supplier Price Compare app
  (single-file HTML/CSS/JS in index.html). Use whenever building, styling, or
  modifying any UI in this project — new sections, cards, buttons, forms,
  styling changes, color or layout tweaks, accessibility fixes — even if the
  user just says "make it look nicer" or "add a screen".
---

# UI/UX Development — Supplier Price Compare

All UI lives in `index.html`: one inline `<style>` block, one `<script>` block, no build step, no dependencies. Never introduce a framework or external CSS/JS unless the user explicitly asks. Edit in place, keep the file self-contained.

## Design tokens (the hallmark)

These custom properties in `:root` are the visual identity. Always reference the variables, never hardcode values:

- `--purple: #5b2a86` — brand/primary: header, selected states, primary emphasis
- `--yellow: #ffc300` — CTA accent: full-width action buttons only
- `--green: #06d6a0` — success/cheapest: winner chips, "best price" highlight
- `--pink: #ef476f`, `--blue: #118ab2` — secondary accents, supplier differentiation
- `--dark: #1d1a2f` — all text
- `--light: #fdf6ff` — page background

Supplier colors come from `COLORS = ["#ef476f", "#118ab2", "#5b2a86"]` in the JS — when adding suppliers, append a new hue there rather than restyling.

## Signature patterns

Match these whenever adding UI; they are what makes the app feel like itself:

- **Cards**: white background, `border-radius: 14px`, soft shadow `0 3px 10px rgba(29,26,47,0.12)`, generous padding.
- **Buttons/inputs**: 12px radius; inputs use `inputMode="decimal"` for money fields.
- **Pills/chips**: `border-radius: 999px`; price chips are tinted with the supplier's color; the winning chip gets a green border/background tint and a ★ marker.
- **CTA**: full-width yellow button, dark text, weight 800, `:active { transform: scale(0.98) }` press feedback.
- **Typography**: `'Segoe UI', system-ui, sans-serif`; base 17px; bold-to-black weights (700–900) for headings and prices; muted hint text `#6b6478` at 13–14px for captions like "Sample data only".
- **Layout**: mobile-first single column; sections numbered "1 ·", "2 ·", "3 ·"; at `@media (min-width: 640px)` widen grids (e.g. price chips go 3 columns).
- **Motion**: subtle only — press scale on buttons, smooth scroll to a section after an action (e.g. scroll to entry form after adding an item). No other animation.

## Behavior conventions

- Re-render via `render()` / `renderInputsOnly()`; when re-rendering on keystroke, preserve input focus — use `renderInputsOnly()` for typing paths.
- Cheapest-price logic is visual too: green = cheapest everywhere, consistently.
- RM currency formatting everywhere money is shown.
- Interactive rows use a `.selected` purple highlight.

## Accessibility baseline (raise it, don't break it)

The current file has semantic `<label>`s but lacks: `:focus-visible` styles, ARIA roles on clickable rows, and keyboard support on `div.item-row` elements. When touching any interactive element:

- Clickable non-buttons get `role`, `tabindex="0"`, and Enter/Space handling, or become real `<button>`s.
- Add `:focus-visible { outline: 2px solid var(--purple); outline-offset: 2px }` when you touch any focusable element's styles.
- Keep color contrast: dark text (`--dark`) on light backgrounds; never put white text on `--yellow` or `--green`.

## Workflow

1. Read the relevant section of `index.html` before editing.
2. Reuse existing classes and tokens before inventing new ones; if a new pattern appears twice, promote it to a class.
3. After editing, open the page in a browser at mobile width (~375px) and desktop (~1280px) to verify layout, then state what you verified.
