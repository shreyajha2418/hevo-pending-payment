# Paid, but no order: pending UPI payment prototype

A clickable, split-screen simulation of a UPI payment that gets stuck "pending" at an online jewellery store, and how the fix handles it.

- **Left:** the customer's phone (product → cart → UPI PIN → debit SMS → pending screen → ticket).
- **Right:** the store backend (orders table, Razorpay events, 15-minute safety-net cron, support ticket) on the same simulated clock.

Illustrative prototype. All data is simulated. "Silver Lane" is a fictional demo store; no real payments, banks or APIs are used.

## Run it
It is one self-contained `index.html` (HTML + CSS + vanilla JS, Google Fonts only). Open it in a browser, or serve it as a static page.

**GitHub Pages:** Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)`. The site appears at `https://<user>.github.io/hevo-pending-payment/`.

## Controls
| Control | What it does |
|---|---|
| Scenario A / B / C | A: payment lands at 10:40 · B: no payment by 12:00 · C: payment lands at 13:10, after the refund message |
| Webhook missed | Scenario A only: the webhook never arrives, the 10:45 cron finds the capture |
| Before / After | Today's behaviour (auto-cancel at 10:15, unmatched money) vs. the fix |
| Play / Next step | Auto-advance, or step through manually while presenting |
| Speed 1× / 5× / 20× | 1, 5 or 20 simulated minutes per real second |
| Reset | Start the scenario again |

Keyboard: `Space` play/pause · `→` next step · `R` reset. You can also tap the pulsing button on the phone to act as the shopper (any 4–6 digit PIN works).

Direct links: `?s=C&m=before`, `?s=A&missed=1`.
