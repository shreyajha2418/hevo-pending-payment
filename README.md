# Paid, but no order: pending UPI payment prototype

A clickable, split-screen simulation of a UPI payment that gets stuck "pending" at an online jewellery store, and how the fix handles it.

- **Left:** the customer's phone (product → cart → UPI PIN → debit SMS → pending screen → ticket).
- **Right:** the store backend (orders table, Razorpay events, 15-minute safety-net cron, support ticket) on the same simulated clock.

Illustrative prototype for Quirksmith. All data is simulated; no real payments, banks or APIs are used.

## Run it
It is one self-contained `index.html` (HTML + CSS + vanilla JS, Google Fonts only). Open it in a browser, or serve it as a static page.

**GitHub Pages:** Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)`. The site appears at `https://<user>.github.io/hevo-pending-payment/`.

## How it works
Pick **A**, **B1** or **B2** from the cards on the left. Everything else plays by itself: a virtual pointer acts as the shopper (Add to cart, Pay with UPI, PIN, "Yes, it was debited"), and the phone and backend advance together on one simulated clock that shows the day as well as the time (Day 0 10:00 … Day 5). Multi-day gaps are fast-forwarded automatically.

| Scenario | What happens |
|---|---|
| A · Confirmed within 2 hours | Captured Day 0 10:40 → order confirmed, ticket closed |
| B1 · Not confirmed in 2 h, money arrives later | 12:00 honest update, ticket stays open → captured 13:10 → order confirmed, ticket updated then closed |
| B2 · Not confirmed in 2 h, money never arrives | 12:00 honest update → Day 3 Razorpay capture window ends → Day 5 order closed (payment failed), ticket auto-closed, shopper told their bank should have returned the money |

A welcome pop-up explains how to use it (pick a card, watch, change speed) and can be closed with ✕, Esc or "Got it". The only other control is **Speed: 1× / 5× / 20×** under the cards.

Click a card again to replay. Direct links that skip the pop-up and auto-start: `?s=A`, `?s=B1`, `?s=B2`.
