# DESIGN — Supplier Price Compare (locked design system)

**Status: locked to the Terrazzo system (v2, 2026-11-17).** This file is the single source of truth for visual design and overrides any project skill on conflict. Implementation: `tokens.css` (all tokens) + `base.css` (reset, controls, states). Any page loads both before its own CSS. Replaces the retired purple/yellow/green token set.

## Material

A materials-library specification voice applied to prices: off-white paper, white cards ruled in 2px ink over a hard offset shadow, wide Syne display heads over a plain Onest body, JetBrains Mono for every measurement (prices, codes, emails, totals). Rust is the one signal. It reads as exact because every edge is hard and every price is set like a figure on a spec sheet.

## Tokens

Read `tokens.css` for values. Summary of the roles:

| Role | Token | Use |
|---|---|---|
| Paper | `--color-paper` (−2, −3) | page ground; wells and bands |
| Plate | `--color-plate` | card surfaces (near-white) |
| Ink | `--color-ink` (−2, `--color-muted`) | text, rules, controls |
| Accent | `--color-accent` | **rust, the only colour**: winner price, primary action, error |
| Focus | `--color-focus` | rings, rust hue, never animated |
| Type | `--font-display` Syne 700 · `--font-body` Onest 400/500 · `--font-mono` JetBrains Mono | two families + one outlier; mono never sets a head or label |
| Radius | `--radius-card: 0` | zero radius everywhere; nothing is round |
| Shadow | `--shadow-card: 14px 14px 0` | hard offset; hover swaps to ink; no blur shadows |

## Rules

1. **Every colour and font through a token.** No literal past `tokens.css`.
2. **Prices, codes, emails, totals: JetBrains Mono, tabular.** Never mono for heads, labels or body.
3. **Rust is a signal, not a fill:** winner price + ★, primary button, error state. Suppliers are identified by mono codes (`SUP-01`) and position, never by hue; their small square swatches exist only on the Suppliers screen.
4. **Winner marking is rust + ★ + position, never colour alone** (a11y).
5. **Cards:** white plate, 2px ink bar, offset shadow; the hover/focus shadow swap is the interaction signature. Depth is never blur.
6. **Dividing:** hairlines for rows and section edges; a paper-2 band at most two per screen; corner ticks as the alternative frame for wells and key figures.
7. **Controls:** ink-filled square primary (one per screen), outlined quiet secondary, rust danger for destructive; all eight states on everything; 44px hit targets; inputs and buttons match height.
8. **Fields:** the border never changes width; focus is an inset ring, reserved transparent at rest; helper lines reserve `min-height: 1.4em`; errors replace the helper in place.
9. **Motion:** transform/opacity only; micro 120ms, short 220ms; hover one signal; one spinner for loading; everything settles instantly under reduced motion.
10. **Accessibility:** `:focus-visible` rings on every interactive element, never `outline: none` without replacement; contrast 4.5:1 body / 3:1 large; keyboard operation for every control; honest empty states (what, why, one action); sample data reads as samples.

## Type scale

`--text-xs` 12 (codes) · `--text-sm` 14 (labels, helpers) · `--text-md` 16 (body) · `--text-lg` 18 (row titles) · `--text-xl` 20 (card heads) · `--text-display-s` 28 (screen heads) · `--text-display` 36 (page head). Hierarchy past scale comes from weight and colour. Heads sentence case, `text-wrap: balance`, tracking `--tracking-display`.

## Screen rules

- One idea per screen; one primary action per screen; numbered flow retired with the old system.
- Every screen defines default, empty, error and loading states (loading = spinner after 300ms, beside the label).
- Density is the design: tables and ledgers before cards-inside-cards; a card in a card never happens.
- Reference comps: `previews/s1-s6-terrazzo.html`, `previews/login-users-terrazzo.html`. These previews are the visual truth for S1–S6 and login/user screens.

## Retired (do not reuse)

Purple/yellow/green/pink/blue hex tokens, 14px-radius cards, soft blur shadows, `999px` pills, the "1 · 2 · 3 ·" numbered section labels, per-supplier chip colours, Segoe UI. They remain only inside `previews/` comps of the old system, if any; treat any sighting in app code as a defect.
