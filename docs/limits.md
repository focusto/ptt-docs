---
title: "Usage & Limits"
description: "API access, usage limits, and billing models for different plans."
category: "guide"
language: "en"
order: 4
showInSidebar: true
---

# Usage & Limits

This document explains the API access rights, usage limits, and billing models for our different plans.

## Plan Breakdown

### Base Plans (Subscriptions)

| Feature | Free Plan | Premium Plan | Enterprise Plan |
| :--- | :--- | :--- | :--- |
| **Monthly Fee** | $0 | $29.9 | **$249** |
| **Monthly Included Calls** | 0 | 10,000 | **100,000** |
| **API Access** | ✅ With credits only | ✅ Included quota + credits | ✅ Included quota + credits |

#### Free Plan
- **Model**: No monthly fee, pay-as-you-go only.
- **Included Quota**: No included monthly API calls.
- **Access**: You can purchase small credit packs (see below) and use the API as long as you have remaining credits.

#### Premium Plan
- **Model**: Subscription-based with a fixed monthly quota.
- **Included Quota**: An active Premium subscription grants you **10,000** API calls per month.
- **Overage**: After 10,000 calls in a billing month, additional usage requires credits from purchased credit packs.

#### Enterprise Plan
- **Model**: Subscription with a large included quota plus pay-as-you-go for additional usage.
- **Included Quota**: The **$249/month** Enterprise plan includes **100,000** API calls.
- **Overage**: After 100,000 calls in a billing month, additional usage is billed against your credit balance.

### Credit Packs (Add-On Usage)

Credit packs let you prepay for additional API calls. One credit equals one API call on the OCR API. Credits do **not** reset monthly and are consumed only when your included monthly quota (if any) has been used.

| Pack Size (Calls) | Price  | Approx. Unit Price | Eligible Plans |
| :--- | :--- | :--- | :--- |
| **1,000** | $3.99  | ~$0.00399 / call | Free, Premium, Enterprise |
| **3,000** | $9.99  | ~$0.00333 / call | Free, Premium, Enterprise |
| **10,000** | $29.9  | ~$0.00299 / call | Premium, Enterprise |
| **50,000** | $134.9 | ~$0.00270 / call | Premium, Enterprise |
| **100,000** | $249  | ~$0.00249 / call | Enterprise only |

**How usage is billed**

1. Each API call increments your **monthly usage counter**.
2. If you have an active subscription (Premium or Enterprise) and have not exhausted your monthly included quota, the call is counted against that quota.
3. Once the monthly quota is used (or if you have no subscription), calls are deducted from your **credit balance**.
4. If you have neither remaining quota nor sufficient credits, API requests will be rejected with an `INSUFFICIENT_CREDITS` error and you will need to purchase more credits or upgrade your plan.

This structure provides a clear path for different usage levels:

- Free users can pay-as-they-go with small packs for occasional usage.
- Premium subscribers get an affordable monthly quota with the option to top up via 10k/50k packs.
- Enterprise customers benefit from a large included quota plus access to high-volume packs with the lowest unit price.
