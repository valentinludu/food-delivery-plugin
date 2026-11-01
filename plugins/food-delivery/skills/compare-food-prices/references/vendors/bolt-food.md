# Bolt Food

- Group / owner: Bolt
- Homepage: https://food.bolt.eu/ — redirects to the user's locale and city, e.g. `/ro-ro/325-bucharest/`.
- Search URL pattern: `https://food.bolt.eu/<locale>/<city-id>-<city>/search?query=<name>` — take `<locale>/<city-id>-<city>` from the URL after the homepage redirect. (Verified 2026-11-01, RO.)
- Results mix restaurants and dishes; scroll to load more and extract restaurant names from page text.
- Login signals: login state is in a cookie page scripts can't read; check the account menu (name/profile = logged in; "Log in" / local equivalent such as "Conectează-te" = logged out).
- Cart / checkout: cart button in the header; fees in the order summary. (To verify.)
- Subscription: Bolt Plus.
- Status: verified (RO, 2026-11-01) for search.
