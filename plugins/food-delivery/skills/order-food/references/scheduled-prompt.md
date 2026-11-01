# Scheduled task prompt template

Fill every field. The scheduled run starts a fresh conversation with no memory of the chat that created it.

```
Scheduled food order (food-price-compare plugin). Follow the "When a scheduled run starts" section of the order-food skill.

Restaurant: {name} (branch: {branch or "any"})
Dishes: {qty}× {dish} ({options}); {qty}× {dish} ...
Preferred app: {one of the user's apps}
User's apps to re-compare: {e.g. Glovo, Wolt, Bolt Food}
Allow switching to a cheaper app: {yes | no}
Prices when scheduled ({date time}): {app} {x}, {app} {y}, {app} {z | not available} {currency} (items + delivery)
Delivery address expected: {address}
Reply timeout: {30} minutes
Rules: re-compare first; build the cart only for these dishes; ask me via push notification before paying and pay only on my explicit yes to the exact app and total; never change payment method, address or tip; report card brand only.
```
