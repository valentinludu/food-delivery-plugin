# food-delivery

A Claude plugin (Claude desktop / Cowork, also Claude Code) that finds which delivery app — **Glovo, Wolt or Bolt Food** — gives the lowest real price for a restaurant, in any city where these apps operate.

It uses the browser the way you would: searches each app (handling name variants like "Pho Bar" / "PhoBar"), reads open/closed status, menu prices and promotions, then — on the app you choose — builds the cart and shows the full fee breakdown. It places the order only on your explicit confirmation and never types passwords or card details.

## Flow

**login → compare → choose app & dishes → cart summary → place order (on explicit yes) → debug**

| Skill | Say |
|---|---|
| `check-food-app-logins` | "Check my food app logins" (one-time setup) |
| `compare-food-prices` | "Which app is cheapest for PhoBar?" — read-only, no cart |
| `order-food` | "Let's go with Glovo" → menu or your dishes → confirm → cart & checkout summary → "yes" to order → debug errors. Also "schedule this for 5 PM". |

## Safety

- Items go into the cart only after you confirm the dish list.
- The order is placed only after you reply "yes" to a confirmation with the exact items, total, address and card brand, re-checked right before pressing Pay. One yes = one order.
- Uses the payment method already selected in the app. Never enters card details, never changes payment method, address or tip. Bank confirmation (3-D Secure) and CAPTCHAs stay with you.
- Card details are never reported beyond the brand (Visa / Mastercard / …). Cookies and tokens are never read out.

## Scheduled orders

Say "schedule this for 5 PM". At that time Claude re-checks prices on all apps, builds the cart on the cheapest allowed app and sends you a push notification asking to confirm the exact total. It pays only after your "yes" (default timeout 30 min, then it cancels). Your computer must be on with the Claude desktop app open.

## Setup

1. Install the plugin. Claude Code: `/plugin install food-delivery --marketplace valentinludu/food-delivery-plugin`. Claude desktop: add the marketplace `valentinludu/food-delivery-plugin` in the plugin settings.
2. Open the built-in browser in Claude desktop (Cmd+Shift+B / Ctrl+Shift+B) and say **"check my food app logins"**. Log in to each app yourself; logins persist.
3. Optional: fill in `skills/compare-food-prices/references/settings.md` (city, apps, preferred branches, default order, timeout).

Browser: Claude desktop built-in browser (preferred) or the Claude in Chrome extension.

## Maintenance (self-healing)

App URLs change. When an entry point in `skills/compare-food-prices/references/apps.md` stops working, Claude falls back to the app's homepage search, finishes the job, and tells you which line to update.

## Disclaimer

Personal-use tool, used at a normal human pace — not a scraper. Prices, fees and promotions change constantly and depend on address and account. Not affiliated with Glovo, Wolt or Bolt.
