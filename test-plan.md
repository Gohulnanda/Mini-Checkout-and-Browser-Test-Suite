# Checkout Test Plan

## Scope
Validate the customer-visible checkout flow for two fixed-price synthetic products. Coverage includes cart changes, total calculations, required-name validation, successful confirmation, empty-cart handling, and rapid repeated submission.

## Risk priorities

| Priority | Risk | Why it matters |
|---|---|---|
| P0 | Duplicate order confirmation after rapid double-click | Could create duplicate orders in a real checkout |
| P0 | Incorrect order total after quantity changes | Customer may be charged or shown the wrong amount |
| P0 | Checkout succeeds with an empty cart or missing name | Invalid order data |
| P1 | Cart contents disappear after validation error | Customer must rebuild the cart |
| P1 | Confirmation/reference missing after success | Customer has no visible proof of submission |

## Automated checks

| ID | Scenario | Expected result | Automated assertion |
|---|---|---|---|
| AT-01 | Add product, enter name, place order | One confirmation and reference are shown | Confirmation visible; reference matches format; count is one |
| AT-02 | Add product, leave name blank, place order | Checkout blocked; error shown; cart retained | Alert text; no confirmation; total remains ₹599 |
| AT-03 | Add two units of Arc Desk Lamp | Line total and order total become ₹2,598 | Exact visible text assertions |

Each automated test starts with a fresh browser page and fresh in-memory application state using `beforeEach`.

## Manual checks to execute and record

Do not mark these as passed until run in a real browser.

### MT-01 — Empty cart
1. Open the checkout in a fresh browser page.
2. Do not add any product.
3. Enter a name.
4. Click **Place order**.
5. Expected: checkout is blocked; a clear empty-cart message appears; no confirmation/reference appears.
6. Record actual result and attach a screenshot.

### MT-02 — Rapid double-click
1. Open a fresh browser page.
2. Add one product and enter a name.
3. Double-click **Place order** rapidly.
4. Expected: only one confirmation and one order reference appear.
5. Record actual result and attach a screenshot.

## Execution record

| Check | Status | Evidence / notes |
|---|---|---|
| AT-01 | Not run in this package | Run with `npm run test:e2e` |
| AT-02 | Not run in this package | Run with `npm run test:e2e` |
| AT-03 | Not run in this package | Run with `npm run test:e2e` |
| MT-01 | Not run | Record after manual browser execution |
| MT-02 | Not run | Record after manual browser execution |

## Defect reporting
No defects are pre-filled. If a reproducible defect is found, record:
- Defect ID and title
- Environment/browser
- Preconditions
- Exact reproduction steps
- Expected result
- Actual result
- Screenshot/video/trace evidence
- Severity and reproducibility

If no defect is found, state that no defect was observed in the tested scope; do not invent one.