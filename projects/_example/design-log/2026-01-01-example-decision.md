# Keep the retry on payment webhooks; require an idempotency key

Date: 2026-01-01 · Status: Implemented · Links: `<ticket>`, `<PR>`

## Background

The payment provider sends a webhook when a charge succeeds. If we don't answer 200 within 10 seconds, it retries, up to 5 times over an hour.

## Problem

A few customers were charged once but got two "order paid" emails, and two shipments were created. Someone proposed turning off provider retries to stop the duplicates.

## Q&A

**Q (agent):** Can we disable retries in the provider settings, since they cause the duplicates?
**A (human):** No. Retries are the only thing that saves us when our service is down or slow during a deploy. Without them we'd lose paid orders, which is far worse than a duplicate email.

**Q (agent):** Does the provider send a stable event ID we can dedupe on?
**A (human):** Yes, `event_id` is the same across retries of the same event.

**Q (agent):** Should a duplicate return an error so the provider stops retrying?
**A (human):** No. Return 200. An error triggers more retries.

## Design

- Keep provider retries on.
- Every webhook handler requires an idempotency key, taken from `event_id`.
- Store processed keys with the order ID. If a key was already seen, return 200 and do nothing.
- The key check and the "mark paid" write happen in one transaction.

## Trade-offs

- An extra table and a write per webhook. Accepted: webhook volume is low.
- Keys kept for 30 days, longer than the provider's retry window. Older duplicates aren't expected.
- Rejected: disabling retries (loses orders), dedup by order ID only (one order can get several legitimate events).

## Implementation Results

_Appended 2026-01-20. The design above is frozen._

- Shipped as planned. Duplicate shipments dropped to zero in the first two weeks.
- Surprise: the provider sometimes sends `charge.succeeded` before `charge.created`. The handler now accepts either order. Detail belongs in `dev/` and is linked from here (see [dev/](../dev/README.md)).
- Follow-up: alert when one key is retried more than 3 times; that points to a slow handler.
