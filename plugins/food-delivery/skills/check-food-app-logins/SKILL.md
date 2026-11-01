---
name: check-food-app-logins
description: >
  This skill should be used when the user asks to "check my food app logins",
  "am I logged in to Glovo/Wolt/Bolt", "set up the food apps", "log in to the delivery apps",
  or before a price comparison when an app appears logged out. Opens Glovo, Wolt and Bolt Food
  in the browser, reports which are logged in, and walks the user through logging in themselves.
metadata:
  version: "0.6.1"
---

# Check food app logins

Confirm the user is logged in to Glovo, Wolt and Bolt Food in the browser used for comparisons, and help them log in where needed. This check is the **gate** for `compare-food-prices` and `order-food`: no searching or price reading happens on an app until it passes. Logins persist in the Claude desktop browser, so logging in is usually a one-time setup.

## Rules

- Never type passwords, SMS/email codes, or verification codes, and never fill login forms. The user logs in themselves.
- Never sign out, change account settings, or read/print cookie or token values.
- Keep the check cheap: one homepage load and one short text extraction per app. Don't search, don't browse menus, don't try to detect the city on a logged-out app.

## Steps

1. Choose the browser exactly as in `compare-food-prices` Step 0 (built-in browser first, Claude in Chrome as fallback). Open each enabled app's homepage from `../compare-food-prices/references/apps.md` (sibling skill folder in this plugin) in its own tab.
2. For each app, run one short JS extraction of the header/top bar text (first ~400 characters) and the delivery address shown. Decide logged in vs logged out from that text only:
   - Glovo: the user's first name in the top-right instead of "Log in".
   - Wolt: an avatar/initials button top-right instead of "Log in" / "Sign up".
   - Bolt Food: the account menu shows the user's name / profile instead of a login prompt in the app's local language (e.g. "Log in", "Conectează-te", "Zaloguj się").
   - **Logged-out signals (any one is enough):** a visible "Log in" / "Sign up" / "Conectează-te" / "Intră în cont" / "Zaloguj się" button, or the account menu offers only login.
   - **Logged in, no address:** the user is logged in but the app shows an "Enter your address" / "Add address" prompt instead of a saved address.
   If still unsure, open the account menu once and read it. If it's still unclear, report "couldn't tell" and treat it as logged out.
3. Report a short status list (logged in / logged out / logged in, no address / couldn't tell) plus the saved delivery address each app shows. The saved default address is the location used for everything; never ask the user for a city.
4. For each logged-out app:
   - In the built-in browser, call `tabs_context`; if the Browser pane is hidden, ask the user to show it (Cmd+Shift+B on Mac, Ctrl+Shift+B on Windows) first.
   - Bring that app's tab forward, open its login screen, then tell the user: "Please log in to <app> in the browser pane (phone + SMS code / email link / Google), then tell me when done."
   - After the user confirms, re-check that tab. Repeat per app.
   For each "logged in, no address" app: ask the user to add their delivery address in that app in the browser pane (Claude doesn't type it), wait for "done", then re-check.
5. Finish with the final status and, if addresses differ between apps, point that out (fees depend on the address).
6. When called as the gate from another skill: return to that skill only for apps that are logged in. Don't continue on logged-out apps unless the user explicitly says to skip them.
