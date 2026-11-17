# Data & Validation Rules — Supplier Price Compare

## Entities
```
SUPPLIERS : [{ name, colour }]  // dynamic, persisted under spc-suppliers.v1 (slice 7)
COLORS    : []          // retired; supplier identity is mono codes (SUP-01…)
items     : { name: string, category: "Grocery"|"Produce"|"Household", prices: (string|number)[] }[]
selected  : number      // index into items
```

## Item form (added slice 3)
- New items are created only through the Add item form (no auto-named rows). Default prices `[10.00, 9.50, 11.00]`.
- Name required, trimmed; blank name blocked with an inline helper error (`aria-invalid` + `aria-live`), never `alert()`.
- Category defaults to "Grocery"; stored per item. Legacy items without `category` read as "Grocery".
- Item code is display-only (`ITM-0{n+1}`), derived from index; it changes if items are reordered or deleted (T11).

## Money
- Display: `RM X.XX`, always 2 decimals (`fmt`).
- Input: `type="number"`, `step="0.01"`, `min="0"`, `inputMode="decimal"`; values stored as entered strings.

## Price validity
A price is valid iff: parses as a finite float AND `>= 0`. Blank, "abc", negative, Infinity → invalid.

## Cheapest determination
- Winner = lowest valid price; **ties go to the first supplier in index order**.
- No valid price for an item → winner index −1 → chip shows "—", result row reads "No valid price" / "—" with `.plain` styling.

## Rendering invariants
- Keystroke updates use `renderInputsOnly()`; the focused input is never destroyed.
- Structural changes (add/select) use full `render()`.
- `prices` array length always equals `SUPPLIERS.length`; adding suppliers must migrate every item.

## Supplier changes (slice 7)
- Rename: indexes stable, prices arrays untouched.
- Add: every item’s prices array gains one empty (unpriced) slot; arrays stay indexed to SUPPLIERS.length.
- Colours live in the swatch set (6 OKLCH hues) and appear only on the Suppliers screen beside each name; winners stay rust + star.

## Defaults
- New item via form: name from the user, category chosen, `prices: [10.00, 9.50, 11.00]`.
- Sample data ships in code; nothing persists (localStorage is a deferred task, key would be `spc.v1`).
