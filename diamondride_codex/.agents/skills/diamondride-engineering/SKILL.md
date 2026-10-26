---
name: diamondride-engineering
description: Implement or review DiamondRide React, FastAPI, Supabase, route recommendation, ML, and hosted vision features against exact requirements, with minimal maintainable code, narrow changes, and verifiable acceptance tests. Use for DiamondRide implementation tasks and code review.
---

# DiamondRide feature implementation

## Workflow
1. Read repository `AGENTS.md` and inspect only the files relevant to the request. Identify existing conventions and contracts before changing code.
2. Convert the user's requirements into an explicit checklist. Preserve all named functions, endpoints, input/output fields, side effects, and edge cases. Distinguish hard requirements from suggestions; do not invent requirements.
3. Define the narrow implementation boundary: which files/functions must change and how the feature will be verified. If something essential is genuinely unspecified, choose the least surprising documented default or ask a focused question when necessary.
4. Implement the smallest clear solution. Reuse existing functions. Do not build unnecessary abstractions, duplicate services, fake integrations, or unrelated improvements.
5. For API integrations, use a provider adapter with validated schemas, configurable credentials, timeouts, and observable errors. Never quietly fall back to fictional data.
6. Test each acceptance criterion, including an ordinary case and material failure/edge cases. Mock external services only in tests; mark live integration verification as incomplete when unavailable.
7. Compare the diff with the original checklist. Explicitly identify anything incomplete. Report only changed files, functionality added, verification, and blockers.

## Project-specific invariants
- Map rendering, geographic trail discovery, candidate route calculation, and final route ranking are distinct responsibilities.
- Never present a route risk score as a probability of being safe. Respect official closures and permissions irrespective of ML predictions.
- The first route recommendation implementation can be rule-based; ML additions require suitable labels and evaluation against that baseline.
- Heavy vision inference is provided through an external service, not FastAPI's CPU server. Maintain swappable providers.
- Bike-photo results are visual observations with uncertainty and physical-check advice, not approval to ride.
- Supabase access must be scoped; frontend never holds secret service-role credentials.

## Requirement-to-test checklist template
Use this internally for feature changes (do not create a file unless asked):

| Requirement | Function or endpoint | Test / verification | Status |
|---|---|---|---|
| Exact user request | Actual implementation location | Concrete test | Complete / Blocked |

## Stop conditions
Do not call a feature complete if a named function is missing, a required field is silently dropped, an external dependency is replaced with a production stub, or the specified behavior has not been checked.
