# Customize prices and plan differences

All pricing is driven by the **`PRICING_PLANS`** array in `facial-harmony-analysis.html`. Find it in the script (search for `PRICING_PLANS`).

**Current setup:** Full = $4.99 USD/month, Pro = $10.99 USD/month. Prices are displayed with "USD" next to the amount. Users must sign in with Google before purchasing a paid plan; the app then applies plan limits (Starter: 10 ratios, no overall score, 2 strengths, 2 improvements; Full/Pro: full access).

---

## 1. Change prices

Edit each plan object:

- **`price`** — number. Use `0` for free.
- **`period`** — `'month'`, `'year'`, or `'forever'`.

Example: change Full to €19/month and Pro to €39/year:

```javascript
{ name: 'Full', price: 19, period: 'month', ... },
{ name: 'Pro',  price: 39, period: 'year',  ... }
```

**Currency:** in the same script, find `var currency = '€'` and set it to `'$'`, `'£'`, etc.

---

## 2. Differentiate plans (what’s included / excluded)

- **`included`** — array of strings. Each item is shown with a **green checkmark** (✓).  
  These are the features **in** this plan.

- **`excluded`** — array of strings. Each item is shown with a **red cross** (✕).  
  Use this to show what this plan does **not** include (e.g. on the free tier: “Overall score”, “70+ ratios”).

**How to differentiate:**

1. **Starter / Free:** few `included` items, and several `excluded` items (e.g. “Overall harmony score”, “Full action plan”) so users see what they get only in paid plans.
2. **Mid tier:** more `included`, no or few `excluded`. This is your “full product” tier.
3. **Top tier:** `included` lists “Everything in [Mid tier]” plus extras (e.g. “Score history”, “Export”, “Priority support”). Leave `excluded` empty.

Example:

```javascript
{
  name: 'Starter',
  price: 0,
  period: 'forever',
  included: ['Side profile score', '10 ratios', 'Basic report'],
  excluded: ['Overall score', '70+ ratios', 'Action plan'],
  ...
},
{
  name: 'Full',
  price: 24.99,
  period: 'month',
  included: ['Overall score', '70+ ratios', 'Full report', 'Action plan'],
  excluded: [],
  ...
}
```

---

## 3. Plan names and “Most popular”

- **`name`** — string shown as the plan title (e.g. "Starter", "Full", "Pro").
- **`featured`** — `true` for one plan to show the **“Most popular”** badge and highlight that card. Use it on the plan you want to push (usually the middle one).

---

## 4. Add or remove a plan

- **Add a plan:** add a new object to the `PRICING_PLANS` array with the same shape (`name`, `price`, `period`, `featured`, `included`, `excluded`, `cta`).
- **Remove a plan:** delete one object from the array.

The layout is a 3-column grid; with 2 or 4 plans it will still work (grid adapts).

---

## 5. CTA button

- **`cta`** — label of the button (e.g. `"Get started"`, `"Choose plan"`). You can set a different label per plan.

To make the button open a link or start checkout, edit the `renderPricingPlans()` function and replace the `<button>` with an `<a href="...">` or add a `data-plan` attribute and a click handler.

---

## 6. Google Sign-In (required for paid plans)

- In the script, set **`GOOGLE_CLIENT_ID`** to your OAuth 2.0 Client ID from [Google Cloud Console](https://console.cloud.google.com/) (APIs & Services → Credentials → Create Credentials → OAuth client ID, type “Web application”, add your site URL to authorized JavaScript origins).
- If `GOOGLE_CLIENT_ID` is empty, the modal shows a “Demo: continue without Google” button so you can test the plan flow; in production you should set a real client ID.
- After sign-in, the user is stored in `localStorage` and the chosen plan is applied. To add real payments (e.g. Stripe), run your checkout after `completePurchase()` or replace the alert with a redirect to your payment page.

---

## 7. Plan limits (how they work)

- **Starter:** Overall harmony score hidden (shows “—”), max 10 measurement ratios in the accordion, max 2 strengths, max 2 improvements, max 2 action plan items. Message: “Upgrade to Full to see your harmony score and 70+ ratios.”
- **Full / Pro:** Full score, all ratios, all strengths and improvements, full action plan.
- Current plan is read from `localStorage` key `ffoids_plan` (`starter` | `full` | `pro`). Changing plan in the Pricing section updates this and the next analysis respects the new plan.

---

## Summary

| What you want          | Where to change it                          |
|------------------------|---------------------------------------------|
| Price amount           | `price` in each plan                        |
| Billing period         | `period`: `'month'` / `'year'` / `'forever'` |
| Currency symbol        | `var currency = '€'` in the script           |
| What’s in the plan      | `included` array                            |
| What’s not in the plan | `excluded` array                            |
| Plan name              | `name`                                      |
| “Most popular” badge   | `featured: true` on one plan                |
| Button text            | `cta`                                       |
