# User Requirements Specification (URS) — Supplier Price Compare

Requirements written in user terms. No technology decisions here; system-level translation lives in `spec.md`.

## U1 — Compare items
As a shopper, I want to see a list of items with each supplier's price side by side, so I can compare at a glance.

- U1.1 Each item shows one price chip per supplier.
- U1.2 The cheapest supplier's chip is visually marked on every item.
- U1.3 Prices are in RM with 2 decimal places.

## U2 — Select and enter prices
As a shopper, I want to tap an item and enter/update each supplier's price, so the comparison reflects reality.

- U2.1 Tapping an item selects it and shows its price entry fields.
- U2.2 I can type a price per supplier; the comparison updates as I type.
- U2.3 Typing must not lose my place (input focus is preserved).
- U2.4 The cheapest field is highlighted while I type.

## U3 — See the cheapest result
As a shopper, I want a clear winner list showing the cheapest supplier and price per item.

- U3.1 Every item appears in the result list with its cheapest supplier and amount.
- U3.2 Items with no valid price show as "No valid price" instead of a wrong answer.

## U4 — Add items
As a shopper, I want to add a new item to compare, so I can grow my list.

- U4.1 One action adds an item and takes me to its price entry.
- U4.2 The new item starts with sensible default prices I can overwrite.

## U5 — Trust and simplicity
- U5.1 The app states clearly that nothing is saved (sample data only).
- U5.2 No sign-up, no loading, works on my phone.

## U6 — Manage suppliers (future)
As a buyer, I want to rename suppliers or add more, so the tool fits my actual suppliers. (Deferred — see tasks.md.)
