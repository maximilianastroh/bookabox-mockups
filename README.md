# BookaBox — Move-out flow mockup

Clickable design prototype for the new **Cancel contract / Move-out flow**.

## 🔗 Open it

**Live:** https://maximilianastroh.github.io/bookabox-mockups/

The page is fully responsive — open it on your phone or desktop, same URL.

## 📱 Test on your phone

Scan this QR (or just paste the URL on your phone):

> Generate one at https://www.qr-code-generator.com or any free QR site
> using the URL above.

## 🧭 What to test

The flow has 3 steps + a confirmation screen. Tap through and check:

1. **Step 1 — Why are you cancelling?**
   - Tap a reason → should highlight with a black border
   - "Continue" should be enabled once a reason is picked

2. **Step 2 — Box state**
   - Tap "Yes, empty" → cleaning question appears
   - Tap "Not yet" → orange warning callout appears, cleaning question hidden, Continue stays disabled
   - Pick a cleaning option

3. **Step 3 — Refund**
   - Pick a saved bank account, OR
   - Tap "+ New account" / "Add a new SEPA account" → form expands, scrolls into view, IBAN field formats as you type
   - Tick the confirmation checkbox
   - Tap "Confirm cancellation"

4. **Confirmation** screen with refund-arrival timeline.

## 🐛 Where to report issues

- Slack: `#design-feedback`
- Or comment directly on the figma/design board: <link>

## 📂 What's in this repo

- `index.html` — the mockup (single self-contained file, no build step)

## ⚠️ Notes

- This is a **design prototype**, not production code. The IBAN field and
  bank lookup are simulated; no data is actually sent anywhere.
- All buttons, navigation, and form inputs are functional.
- Restart the demo from the confirmation screen via "↻ Restart demo".
