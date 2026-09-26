---
name: telephonist
description: Connect and inspect your Telephonist. Use when choosing a phone service or checking its current state.
---

1. Call `list_telephonists`. If no connection exists, call `connect_telephonist` and show the returned approval link. Request update access only when the owner wants to change the service.
2. The owner must sign in and approve the Telephonist connection. Do not treat an approval link as a completed grant.
3. List again after approval. Select an explicitly connected Telephonist; clarify the selection if ambiguous.
4. Call `get_telephonist` and report its actual configuration and runtime state. This is the same service and owner grant used by ChatGPT V2.
5. For a change, use the brief workflow. Teammate delegation is not a substitute for a Telephonist update.
