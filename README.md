# Mini Checkout and Browser Test Suite

A small React + TypeScript checkout demo and Playwright browser test suite for the Fynd SDET Intern challenge.

## Features
- Two synthetic products with fixed INR prices
- Add products, change quantities, and remove products
- Live line totals and order total
- Required customer name validation
- Empty-cart validation
- Order confirmation with a generated reference
- Synchronous submission lock to prevent rapid duplicate submissions
- Three Playwright browser tests

No backend, database, payment provider, or external service is used.

## Requirements
- Node.js 20 or later (Node.js 18.18+ may also work with compatible npm)
- npm
- Chromium browser installed by Playwright

## Run locally

```bash
npm install
npx playwright install chromium
npm run dev
```

Open the local URL printed by Vite (normally http://localhost:5173).

## Run the browser tests

```bash
npm run test:e2e
```

Playwright starts the Vite app on `http://127.0.0.1:4173` automatically. The three tests each navigate to a fresh page before execution.

Open the HTML report:

```bash
npm run test:e2e:report
```

For interactive test debugging:

```bash
npm run test:e2e:ui
```

## Production build

```bash
npm run build
npm run preview
```

## Test coverage

1. Successful checkout displays a confirmation and order reference.
2. Blank required name blocks checkout and preserves the cart.
3. Increasing quantity updates the exact line and order totals.

Manual empty-cart and rapid double-click steps are in [`test-plan.md`](./test-plan.md). Execute them in a browser and update the execution record with actual results and evidence before submission.

## Design decisions
- Prices are integer INR values to avoid floating-point currency arithmetic for these fixed-price examples.
- The submit handler validates cart and trimmed customer name before submission.
- A React ref is used as a synchronous lock because state updates alone may not prevent two clicks occurring before the next render.
- The lock remains set after a successful submission. The confirmation view prevents another submission until the user deliberately starts a new order.
- The order operation is simulated locally with a short timeout; this is not a real order/payment system.

## Submission checklist
- [ ] `npm install` completes
- [ ] `npm run build` passes
- [ ] `npm run test:e2e` passes
- [ ] Manual empty-cart check executed and recorded
- [ ] Manual rapid double-click check executed and recorded
- [ ] Screenshots or Playwright report attached
- [ ] README and test plan reflect actual execution results
