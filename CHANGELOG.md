# Changelog

## 0.7.0
- European vendors: per-vendor registry in `references/vendors/` (Glovo, Wolt, Bolt Food verified; Uber Eats, Deliveroo, Just Eat Takeaway brands, foodora, efood, Foody, Yemeksepeti unverified) with a generic method and a template for adding more.
- "My apps" setting: only the user's apps are opened and only their vendor files are read (asks once if empty).
- Apps are resolved before any tab opens: named in message → "My food apps" profile preference → settings → memory → ask once "Which delivery apps do you use?" (only if the user doesn't know or gives a country, Claude web-searches the current main apps there and confirms). Never opens apps outside the list, max 4 per run.
- No country lists in the plugin (they change too often); vendor files hold only how each site works.
- Report columns follow the user's apps. `apps.md` replaced by `vendors/` (old file left as a pointer; delete it).

## 0.6.1
- Login gate first: no searching or price reading on an app until it's confirmed logged in; logged-out apps stop immediately and the user is asked to log in (logged-out pages show the wrong city and higher/generic prices).
- Cheaper login check (one page load + short text extraction per app) with clear logged-out signals.
- Efficiency budget: max 3 search attempts per app, short text extraction, stop after 3 calls without progress, never browse to work out the city.
- `order-food` runs the login gate before building a cart in new or scheduled sessions.
- Location always comes from each app's saved default address: never asks or waits for a city. If a logged-in app has no saved address and asks for one, the user is asked to add it in the app. Removed the city/address settings.

## 0.6.0
- Plugin renamed to `food-delivery` (it compares, orders and schedules, not only compares prices). Skills: `food-delivery:check-food-app-logins`, `food-delivery:compare-food-prices`, `food-delivery:order-food`.
- Repository renamed to `food-delivery-plugin`.

## 0.5.0
- Renamed (from `food-price-compare`); works in any city served by Glovo, Wolt or Bolt Food (no longer Bucharest-only).
- Country/city and timeout settings; currency taken from the apps; local-language button names.
- Packaged as a GitHub plugin marketplace.

## 0.4.0
- Scheduled orders: re-compare at run time, build cart, ask via push notification, pay only on explicit yes, timeout cancels.

## 0.3.0
- Can place the order from chat after an explicit yes to the exact items, total, address and card brand; re-checks before pressing Pay.

## 0.2.0
- Split into login → compare (read-only) → choose dishes → cart summary → debug. Cart only after confirmation. Card brand only.

## 0.1.x
- Initial comparison skill, login check, settings, self-healing entry URLs; cart-page fee reading.
