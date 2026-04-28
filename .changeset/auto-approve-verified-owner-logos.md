---
---

Brand logos uploaded by a verified domain owner auto-approve and rebuild the manifest immediately, instead of sitting in the pending review queue. Closes #3150.

Concretely: when `POST /api/brands/:domain/logos` runs, we check `isVerifiedBrandOwner(user.id, domain)` (existing helper, now exported) and set `source: 'brand_owner', review_status: 'approved'` if true. Verified hosted brands skip the manifest rebuild because they manage logos via brand.json.

Note: community uploads were subsequently extended to also auto-approve in #2568 — the pending queue no longer queues any new uploads.
