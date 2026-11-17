# Task Breakdown — Supplier Price Compare

Ordered tasks, each with acceptance criteria. Verify manually at 375px and 1280px widths (see plan.md). Traceability to `spec.md` in brackets.

## Phase 1 — Core loop polish (current single page)

### T1. Accessibility baseline pass — done (slices 1–2) ✅ done (slices 1–2) [SR-7 baseline]
- Make item rows keyboard-activatable: `role="button"`, `tabindex="0"`, Enter/Space selects.
- Add global `:focus-visible` outline (2px solid var(--purple), offset 2px).
- ✅ All interactive elements operable by keyboard alone; focus visible on every control.

### T2. Input validation & error states — done (slice 8) ✅ done (slice 8) [SR-2.4, SR-3.2]
- Invalid/blank price → chip shows "—" and result row shows "No valid price".
- ✅ Entering "abc", "-5", empty leaves highlights correct and never a wrong winner.

### T3. Tie-breaking rule — done (slice 8) ✅ done (slice 8) [SR-1.2]
- Explicit: first supplier in order wins a tie. Document in code.
- ✅ Two identical lowest prices mark the earlier supplier's chip.

### T4. Empty state — done (slice 1, empty-card pattern) ✅ done (slice 1, empty-card pattern) [U5]
- When no items: item list shows an honest empty message + the Add action.
- ✅ Deleting/starting with zero items never shows a blank page.

## Phase 2 — Restructure into screens (per screens.md)

### T5. Price Entry as full-screen sheet [SR-2]
- Move section 2 into a sheet/screen opened from a selected item.
- ✅ Add item → entry sheet opens → typing works → close returns to list, selection kept.

### T6. Cheapest Result as shopping-list screen [SR-3]
- Winner list becomes its own screen with running total and copy-list action.
- ✅ Total equals sum of winners; copy action yields readable text.

### T7. Add/Edit Item form — done (slice 3) ✅ done (slice 3) [SR-4]
- Replace auto-named "New Item N" with a form (name + optional category), inline validation.
- ✅ Blank name blocked with inline error; no browser alerts.

## Phase 3 — Deferred (requires re-plan per plan.md)

### T8. Items catalog screen (search, last-best supplier per row)
### T9. Supplier management — done (slice 7) ✅ done (slice 7) (rename/recolor/add; `prices` array must stay indexed to `SUPPLIERS.length`) [SR-7.1]
### T10. localStorage persistence — done (slice 8) ✅ done (slice 8), versioned key, clear-data control, updated notice [SR-7.2]
### T11. Delete/rename items [SR-7.3]

## Rule for AI agents
One task per change; read `DESIGN.md` before any visual work; do not skip acceptance criteria; if a task fires an architecture trigger (plan.md), stop and re-plan.
