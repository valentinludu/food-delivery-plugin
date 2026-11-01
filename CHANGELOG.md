# Changelog

## 0.5.0
- Renamed to `food-delivery-price-compare`; works in any city served by Glovo, Wolt or Bolt Food (no longer Bucharest-only).
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
