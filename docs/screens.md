# Screen Inventory — Supplier Price Compare

One idea per screen; one primary action per screen. State colors universal: green = cheapest, purple = selected, yellow = action. Build order: S1 → S3 → S4 → S2 → S5 → S6.

## S1 · Compare (home)
- **Purpose**: see all items and each supplier's price at a glance.
- **Primary action**: "+ Add Item" (yellow CTA).
- **Content**: item rows with supplier price chips; winner chip starred.
- **States**: default (sample items) · empty (no items → message + Add CTA) · typing (winners update live).
- **Current status**: built (slices 1–2, 6): Terrazzo ledger, hash-routed home.

## S2 · Add/Edit Item
- **Purpose**: capture item name (and optional category) fast.
- **Primary action**: "Save".
- **States**: blank form · validation error (inline, never alert) · editing existing item.
- **Current status**: built (slice 3).

## S3 · Price Entry (sheet)
- **Purpose**: enter/update all supplier prices for one selected item.
- **Primary action**: done/close (values save on keystroke).
- **Content**: selected item name header; one decimal input per supplier; cheapest field green.
- **States**: no selection ("—") · typing (focus preserved, highlights update) · all-blank prices.
- **Current status**: built (slices 2, 6): wells + Lowest band, reachable from Catalog.

## S4 · Cheapest Result / Shopping List
- **Purpose**: what to buy and where — winner per item.
- **Primary action**: copy list.
- **Content**: per item: name, winning supplier, RM amount, green highlight; running total.
- **States**: all priced · some items "No valid price" (plain rows) · empty list.
- **Current status**: built (slice 2): winner table + totals band + Copy list.

## S5 · Items Catalog
- **Purpose**: find any past item and its last-best supplier.
- **Primary action**: search.
- **States**: populated · no matches · empty.
- **Current status**: built (slice 6): search, grid, no-match add.

## S6 · Suppliers (settings)
- **Purpose**: manage supplier names/colors/count.
- **Primary action**: edit supplier.
- **States**: three defaults · edited · added suppliers (append color from palette).
- **Current status**: built (slice 7): rename, swatches, add, migration.

## Cross-cutting
- **Error**: invalid prices never crash render; shown as "No valid price".
- **Trust notice**: "Sample data only — nothing is saved" visible on home until persistence ships (T10 changes it).
