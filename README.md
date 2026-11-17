# Supplier Price Compare

A lightweight, mobile-first web app for comparing grocery prices across suppliers — built for Malaysian shoppers and small buyers who want to know, instantly, where to buy each item cheapest.

**No backend. No accounts on a server. No build step.** One HTML file plus two stylesheets, everything stored on your own device.

## What it does

- **Compare** — every item with each supplier's price side by side; the cheapest source is marked in rust with a star, everywhere.
- **Price entry** — tap an item, type each supplier's price; highlights and results update on every keystroke without losing your place.
- **Winners** — a clean list of the cheapest supplier per item with a running total and a copy-list action.
- **Catalog** — search every item you've priced; no match? Add it in one go.
- **Suppliers** — rename suppliers, assign colours, add new ones; every item's prices migrate safely.
- **Users** — simple device-local accounts with owner / editor / viewer roles. Viewers see the prices but can't change them.

Everything saves automatically to your device's local storage. Nothing is sent anywhere — the header tells you so.

## Running it

No install, no build. Open `index.html` in a browser, or serve the folder:

```
npx http-server
```

Then visit the printed URL. Works on a phone (375px) and desktop.

## The look

The UI follows **Terrazzo**, a locked design system (see [`DESIGN.md`](DESIGN.md)): off-white paper, ink-ruled white cards with hard offset shadows, Syne display heads, JetBrains Mono for every price, and rust as the one colour that means something — the winner. It's designed to look made, not generated.

## Documentation

| Doc | What it holds |
|---|---|
| [`docs/brief.md`](docs/brief.md) | vision, audience, success criteria |
| [`docs/URS.md`](docs/URS.md) | user requirements as user stories |
| [`docs/spec.md`](docs/spec.md) | system requirements (SR-1 … SR-9) |
| [`docs/plan.md`](docs/plan.md) | architecture decisions and re-plan triggers |
| [`docs/data-rules.md`](docs/data-rules.md) | data model, validation, tie-breaking |
| [`docs/screens.md`](docs/screens.md) | screen inventory with states |
| [`docs/tasks.md`](docs/tasks.md) | task breakdown and statuses |

## Honest limits

- **Demo auth**: accounts and passwords (salted-hashed) live in your browser's local storage on this device only. This protects casual inspection, not a determined attacker — there is no server.
- **Clearing browser data** erases your items, suppliers, and accounts.
- Sample data ships in the code; use **Clear all data** (Suppliers screen) to return to it.

## Stack

Vanilla HTML / CSS / JavaScript. Zero dependencies, zero frameworks. The design system lives in `tokens.css` + `base.css`; the app in `index.html`.
