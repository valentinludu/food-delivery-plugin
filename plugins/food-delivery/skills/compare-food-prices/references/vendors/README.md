# Vendor registry

Each supported delivery app has one file here. Skills load **only the files for the apps the user uses** (see `../settings.md` → "My apps"), never all of them.

| Vendor | File | Group | Main domain | Status |
|---|---|---|---|---|
| Glovo | glovo.md | Delivery Hero | glovoapp.com | verified (RO) |
| Wolt | wolt.md | DoorDash | wolt.com | verified (RO) |
| Bolt Food | bolt-food.md | Bolt | food.bolt.eu | verified (RO) |
| Uber Eats | uber-eats.md | Uber | ubereats.com | unverified |
| Deliveroo | deliveroo.md | DoorDash | deliveroo.co.uk / deliveroo.fr / … | unverified |
| Just Eat Takeaway brands | just-eat-takeaway.md | Prosus | just-eat.co.uk, lieferando.de, thuisbezorgd.nl, pyszne.pl, takeaway.com, … | unverified |
| foodora | foodora.md | Delivery Hero | foodora.se, foodora.no, foodora.at, foodora.cz, foodora.hu, … | unverified |
| efood | efood.md | Delivery Hero | e-food.gr | unverified |
| Foody | foody.md | Delivery Hero | foody.com.cy | unverified |
| Yemeksepeti | yemeksepeti.md | Delivery Hero | yemeksepeti.com | unverified |

This plugin doesn't track which countries each app serves, because that changes often (acquisitions, exits, rebrands). The user's logged-in app is the source of truth: if it delivers to their saved address, it's available.

**Status:** `verified (<country>)` = the entry URLs, search method and login signals were tested there. `unverified` = best-known starting point; follow the generic method below and report what actually worked in a "Plugin maintenance" note so the file can be updated.

## Which apps to open (never all of them)

Most countries have about 3 main apps. Open **only the user's apps**, resolved in this order (stop at the first that gives a list):
1. Apps named in the user's message ("compare on Glovo and Wolt").
2. Memory: a saved preference or earlier answer visible in the conversation context (the user's Claude profile preferences / instructions, memory, or earlier in this chat), e.g. "My food apps: Glovo, Wolt, Bolt Food". If found, use it without asking.
3. "My apps" in `../settings.md`.
4. Otherwise **ask once, before opening anything**: "Which delivery apps do you use?" Ask only this — don't ask for the country.
   - Only if the user doesn't know, isn't sure, or answers with a country/city instead of apps: **web-search** the main food delivery apps available there right now (e.g. "main food delivery apps in <country> <current year>"), check that the results are recent, and show the 2–4 leading apps. Ask the user to confirm which of them they use before opening any. Don't rely on your own background knowledge of which apps exist there — availability changes. If no web search tool is available, ask the user to name their apps.
   - After the user answers, suggest saving it so it isn't asked again: add "My food apps: …" to their Claude profile preferences.

Hard limits: never open an app that isn't in the resolved list; never open more than 4 apps in one run unless the user explicitly asks; never "try" other vendors to see if they work.


## Generic method (works for any vendor)

1. **Open** the vendor's homepage for the user's country. The logged-in app redirects to the user's saved address.
2. **Login check:** account name/initials/menu in the header = logged in; a "Log in" / "Sign up" button (any language) = logged out; "Enter your address" while logged in = no address.
3. **Search:** try the site's search URL if listed; otherwise click the visible search box, type the name, press Enter. Max 3 attempts (name variants).
4. **Restaurant page:** read status, prices, promos, delivery fee, minimum order with short text extraction.
5. **Cart / checkout:** cart or basket button in the header; fees appear in the cart or the checkout summary. Never press the final order button without the user's explicit yes (see `order-food`).

## Adding a vendor

Copy `_template.md`, fill it in, add a row above. Mark it `unverified` until a real run confirms it.
