# App entry points and quirks

Supported vendors: **Glovo, Wolt, Bolt Food**. Each operates in a different set of countries and cities; an app that doesn't serve the user's city is skipped.

Update this file when an entry point stops working (see "Self-healing" in SKILL.md). Note the date and city where each line was last verified.

## Location = the app's saved default address

- Never ask the user for a city and never browse to work it out. Each app already uses the default delivery address saved in the user's account; read it from the header and use it.
- Only if a logged-in app has no saved address and asks for one: ask the user to add their address in that app (in the browser pane), then continue. Don't type the address yourself.
- Apps localize URLs and UI language by country. Prefer English UI where offered, but expect local-language labels (cart, checkout, login).

## Login signals (quick check)
- Logged in: user's name/initials or account menu in the header, and the user's saved delivery address shown.
- Logged out: "Log in" / "Sign up" / local-language equivalent visible. Stop and ask the user to log in.
- Logged in but no address: an "Enter your address" / "Add address" prompt. Ask the user to add their address in the app.

## Bolt Food
- Homepage: https://food.bolt.eu/ — redirects to the user's locale and city, e.g. `/ro-ro/325-bucharest/`.
- Search URL pattern: `https://food.bolt.eu/<locale>/<city-id>-<city>/search?query=<name>` — take `<locale>/<city-id>-<city>` from the URL after the homepage redirect. (Verified 2026-11-01, Bucharest.)
- Results mix restaurants and dishes; scroll to load more and extract restaurant names from page text.
- Login state is held in a cookie page scripts cannot read; check login via the account menu instead.
- Cart: cart button in the header; fees appear in the order summary. (To verify per city.)

## Wolt
- Homepage: https://wolt.com/en/discovery (uses the user's saved address).
- Search URL: `https://wolt.com/en/search?q=<name>` (Verified 2026-11-01, Bucharest.)
- Restaurant URL pattern: `https://wolt.com/en/<country-iso3>/<city>/restaurant/<slug>` (e.g. `/en/rou/bucharest/...`).
- Search results load lazily: scroll to the bottom, then match `<a>` link text.
- Restaurant header shows status ("Closed · Opens at 12:00"), min. order and delivery fee.
- Cart: basket button ("View order"); delivery and service fee shown in the order summary before payment. (To verify.)

## Glovo
- Homepage: https://glovoapp.com/en (uses the user's saved address).
- Search: URL query parameters do NOT work reliably. Open the homepage, click the search box, type the name, press Enter. (Verified 2026-11-01, Bucharest.)
- Store URL pattern: `https://glovoapp.com/en/<country-iso2>/<city>/stores/<slug>` (e.g. `/en/ro/bucharest/...`).
- Store header shows promo badge (e.g. "-30% select items"), delivery fee (struck through if free) and "Schedule for Tomorrow" when closed.
- Discounted items show two prices: discounted first, original second.
- Cart: "Your order" panel on the store page; fees shown after continuing to the checkout summary. (To verify.)
