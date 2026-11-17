# System Requirements Specification (SRS) — Supplier Price Compare

Translates `URS.md` into testable system requirements. Traceability: [U1.1] → SR-1, etc.

## SR-1 Item list (U1)
- SR-1.1 Render one row per item: name (weight 800) + one price chip per supplier, colored from `COLORS`.
- SR-1.2 The chip of the supplier with the lowest valid price gets class `win` (★ marker). Ties: first supplier in order wins.
- SR-1.3 All money displayed as `RM X.XX` (`fmt()`).

## SR-2 Price entry (U2)
- SR-2.1 Exactly one item is selected at a time; selection is shown with `.selected` styling.
- SR-2.2 Price inputs: `type="number"`, `step="0.01"`, `min="0"`, `inputMode="decimal"`.
- SR-2.3 Every keystroke updates cheapest-highlight and results via `renderInputsOnly()`; the focused input is never rebuilt.
- SR-2.4 Stored price values are the raw input strings; validity = parses as float, `>= 0`, not NaN.

## SR-3 Results (U3)
- SR-3.1 One result row per item: item name, winning supplier name, winning amount.
- SR-3.2 No valid price → row shows "No valid price" and "—", styled `.plain`.

## SR-4 Add item (U4)
- SR-4.1 Add button appends `{ name: "New Item N", prices: [10.00, 9.50, 11.00] }`, selects it, re-renders, smooth-scrolls to the entry section.

## SR-5 Data model (U1, U2)
```
SUPPLIERS = ["Klang Import Sdn Bhd", "Pasar Malam Trading", "JB Wholesale"]
COLORS    = ["#ef476f", "#118ab2", "#5b2a86"]
items     = [{ name: string, prices: [string|number × suppliers.length] }]
selected  = index into items
```
- SR-5.1 `cheapestOf(item)` returns the winning index or −1.
- SR-5.2 Chip labels use the supplier's first word only.

## SR-6 Constraints (U5)
- SR-6.1 Single `index.html`, no dependencies, no build step, no persistence, no network calls.
- SR-6.2 Header permanently displays "Sample data only — nothing is saved".

## SR-8 Authentication and users (Slice 4, demo scope)
- SR-8.1 Accounts live in localStorage under `spc-auth.v1` (`{ users: [{ name, email, salt, hash, role }] }`); sessions under `spc-session.v1` (`{ email }`). No network calls, ever.
- SR-8.2 Passwords are salted SHA-256 (`crypto.subtle.digest`, random 16-byte salt, `salt:password` domain). Demo grade: protects casual device inspection, not a determined attacker.
- SR-8.3 Roles: `owner` | `editor` | `viewer`. The first account created becomes `owner`; later accounts default `editor`.
- SR-8.4 The app is gated behind a session: `authView` shows when no valid session, `appView` when signed in. Sign-out removes the session key.
- SR-8.5 Error copy states what happened and what to do ("No account with this email on this device. Create one below."), never which of email/password was wrong beyond that.
- SR-8.6 The header notice stays honest: accounts and data live on this device only. When persistence (SR-7.2) lands, the notice changes to say so.
- SR-8.7 Duplicate email on create is rejected with an inline error pointing to sign-in.
- SR-8.8 Users screens (owner only): a ledger of accounts with role badges, per-user role management (owner/editor/viewer), invite (creates the account locally with a shared password; states plainly that no email is sent), and removal with a one-step arm-then-confirm on the button itself.
- SR-8.9 The signed-in owner cannot demote or remove themselves; the Owner radio and Remove control are disabled with a stated reason.
- SR-8.10 Viewer role is read-only: Add Item, Copy list and the Users screen are hidden or disabled, a visible read-only note replaces the header notice, and state is conveyed by text plus disabled channels, never colour alone.
- SR-8.11 Invite copy shares the password through the owner ("Share it with them yourself"); the demo never sends email.
- SR-7.1 Dynamic supplier list (add/rename/recolor) — data model must keep `prices` indexed to `SUPPLIERS.length`.
- SR-7.2 Persistence — DONE in slice 8 (see SR-9).
- SR-7.3 Delete/rename items.

## SR-7 Future requirements (U6, deferred)
- SR-7.1 Dynamic supplier list (add/rename/recolor) — data model must keep `prices` indexed to `SUPPLIERS.length`.
- SR-7.2 Persistence — DONE in slice 8 (see SR-9).
- SR-7.3 Delete/rename items.

## SR-9 Persistence (slice 8)
- SR-9.1 Items persist in localStorage under `spc.v1`; writes are debounced 300ms after any mutation (price input, item save).
- SR-9.2 Loaded data is validated (names/categories are strings, prices an array of strings/numbers); invalid or absent data falls back to the sample list with fresh copies.
- SR-9.3 A Clear-all-data control on the Suppliers screen arms then confirms on the button itself, resets items to the sample list, and reports the result in a note; suppliers and accounts are untouched.
- SR-9.4 The header notice now reads "Saved on this device. Nothing leaves your phone." — honest about persistence and the device-only scope.
- SR-9.5 Tie-breaking is explicit: equal lowest prices resolve to the first supplier in index order (code comment in cheapestOf).
- SR-9.6 Invalid prices render as "none yet" chips and "No valid price" result rows everywhere, including the copy-list output.
## SR-9 Persistence (slice 8)
- SR-9.1 Items persist in localStorage under `spc.v1`; writes are debounced 300ms after any mutation (price input, item save).
- SR-9.2 Loaded data is validated (names/categories are strings, prices an array of strings/numbers); invalid or absent data falls back to the sample list with fresh copies.
- SR-9.3 A Clear-all-data control on the Suppliers screen arms then confirms on the button itself, resets items to the sample list, and reports the result in a note; suppliers and accounts are untouched.
- SR-9.4 The header notice now reads "Saved on this device. Nothing leaves your phone." — honest about persistence and the device-only scope.
- SR-9.5 Tie-breaking is explicit: equal lowest prices resolve to the first supplier in index order (code comment in cheapestOf).
- SR-9.6 Invalid prices render as "none yet" chips and "No valid price" result rows everywhere, including the copy-list output.