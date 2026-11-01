---
name: check-food-app-logins
description: >
  This skill should be used when the user asks to "check my food app logins",
  "am I logged in to Glovo/Wolt/Bolt", "set up the food apps", "log in to the delivery apps",
  or before a price comparison when an app appears logged out. Opens Glovo, Wolt and Bolt Food
  in the browser, reports which are logged in, and walks the user through logging in themselves.
metadata:
  version: "0.5.0"
---

# Check food app logins

Confirm the user is logged in to Glovo, Wolt and Bolt Food in the browser used for comparisons, and help them log in where needed. Logins persist in the Claude desktop browser, so this is usually a one-time setup.

## Rules

- Never type passwords, SMS/email codes, or verification codes, and never fill login forms. The user logs in themselves.
- Never sign out, change account settings, or read/print cookie or token values.

## Steps

1. Choose the browser exactly as in `compare-food-prices` Step 0 (built-in browser first, Claude in Chrome as fallback). Open each enabled app's homepage from `../compare-food-prices/references/apps.md` (sibling skill folder in this plugin) in its own tab.
2. For each app, decide logged in vs logged out from visible page text only:
   - Glovo: the user's first name in the top-right instead of "Log in".
   - Wolt: an avatar/initials button top-right instead of "Log in" / "Sign up".
   - Bolt Food: the account menu shows the user's name / profile instead of a login prompt in the app's local language (e.g. "Log in", "Conectează-te", "Zaloguj się").
   If unsure, open the account menu and read it; don't guess.
3. Report a short status list (logged in / logged out / couldn't tell) plus the delivery address each app shows.
4. For each logged-out app:
   - In the built-in browser, call `tabs_context`; if the Browser pane is hidden, ask the user to show it (Cmd+Shift+B on Mac, Ctrl+Shift+B on Windows) first.
   - Bring that app's tab forward, open its login screen, then tell the user: "Please log in to <app> in the browser pane (phone + SMS code / email link / Google), then tell me when done."
   - After the user confirms, re-check that tab. Repeat per app.
5. Finish with the final status and, if addresses differ between apps, point that out (fees depend on the address).
