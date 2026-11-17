# Technical Plan — Supplier Price Compare

## Architecture decision: stay single-file
Keep `index.html` (HTML + inline CSS + inline vanilla JS) for the current scope. Rationale: no backend, no build tooling, instant load, zero maintenance overhead. Revisit only when a trigger fires (see Triggers below).

## Structure rules (if the file grows past ~600 lines)
Split without a build step:
```
index.html
styles.css   (link in <head>)
app.js       (script before </body>)
```
Order: extract CSS first, then JS. DOM structure stays in the HTML.

## State management
- Single in-memory arrays: `items`, `selected`, module constants `SUPPLIERS`, `COLORS`.
- Render model: full re-render `render()` on structural changes (add/select); `renderInputsOnly()` on keystrokes — never rebuild the focused input.
- No frameworks, no reactivity libraries.

## Storage
None today (SR-6.1). If persistence is approved later: `localStorage` under a versioned key (`spc.v1`), written on input debounce (300ms), validated on load, with a "Clear data" control and updated header notice.

## Browser targets
- Evergreen Chrome/Edge/Safari/Firefox, mobile-first (375px) and desktop (1280px).
- No transpilation; ES6 features only (already in use: arrow functions, template literals).

## Testing approach
Manual verification per task: open in browser at 375px and 1280px, check the acceptance criteria in `tasks.md`. No test framework while single-file.

## Triggers to re-plan architecture
- Persistence or multi-list support (needs storage layer + migration).
- More than ~4 screens (needs real routing/structure).
- Any backend/API need (needs full re-plan).

## Dependencies policy
None. No CDN fonts, no icon packs, no polyfills. System font stack only.
