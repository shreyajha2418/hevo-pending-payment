# Paid, but no order: pending UPI payment prototype

A clickable, split-screen simulation of a UPI payment that gets stuck "pending" at an online jewellery store, and how the fix handles it.

- **Left:** the customer's phone (product → cart → UPI PIN → debit SMS → pending screen → ticket).
- **Right:** the store backend (orders table, Razorpay events, 15-minute safety-net cron, support ticket) on the same simulated clock.

Illustrative prototype. All data is simulated. "Silver Lane" is a fictional demo store; no real payments, banks or APIs are used.

## Run it
It is one self-contained `index.html` (HTML + CSS + vanilla JS, Google Fonts only). Open it in a browser, or serve it as a static page.

**GitHub Pages:** Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)`. The site appears at `https://<user>.github.io/hevo-pending-payment/`.

## How it works
Pick **A**, **B** or **C** from the cards on the left. Everything else plays by itself: a virtual pointer acts as the shopper (Add to cart, Pay with UPI, PIN, "Yes, it was debited"), and the phone and backend advance together on one simulated clock.

| Scenario | What happens | Runtime |
|---|---|---|
| A · Payment arrives late, within 2 hours | Captured at 10:40 → order confirmed, ticket closes itself | ~45 s |
| B · No payment by the 2-hour mark | 12:00 → "money back in 3–5 days", Pay unlocked | ~65 s |
| C · Payment arrives after 2 hours | Refund message at 12:00, captured at 13:10 → order confirmed anyway | ~85 s |

Click a card again to replay. Direct link that auto-starts a scenario: `?s=B`.
