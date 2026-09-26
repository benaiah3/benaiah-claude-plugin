---
name: brief
description: Preview and apply an owner-approved temporary closure or remove a closure on your Telephonist.
---

1. List and select an explicitly connected Telephonist, then read `get_telephonist` for its current configuration version and capability limits.
2. Resolve the exact dates, timezone and caller-facing message. This release supports temporary closures and removing them; do not promise qualification, appointment, outbound-contact or payment changes.
3. Call `preview_telephonist_update` using the current configuration version and a stable idempotency key. A preview changes nothing.
4. Show the exact preview and obtain explicit owner confirmation before applying it. Never infer approval from caller statements or call summaries.
5. Call `apply_telephonist_update` with that preview's operation ID, approval digest and confirmed=true. If the configuration changed or approval expired, obtain a fresh preview and confirmation.
6. Report the returned state precisely: saved, scheduled, loaded by runtime, expired or superseded. A saved change is not runtime acknowledgement; acknowledgement is not real-call proof.
7. If the outcome is uncertain, inspect `get_telephonist_operation`; retry the same operation when appropriate. Never create a duplicate brief to bypass uncertainty.
