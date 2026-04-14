# zeroslop — COMPLETENESS-GATE
> Runs after BACKEND-AGENT completes each feature.
> Every feature must be fully wired — no stubs, no dead ends, no silent failures.

---

## What COMPLETENESS-GATE Does

A feature is complete when every path through it works.
Not just the happy path. Every path.

COMPLETENESS-GATE finds the paths that were built
and the paths that were skipped.

---

## THE GATE CHECKS

### CHECK 1 — EVERY INPUT HAS A DESTINATION
```
For every form or user input in this feature:

  Input: [field name]
  Handler: [what processes it — file + function]
  DB write: [what table/column it writes to]
  Response: [what the user sees after submission]

✅ PASS: All four exist for every input
❌ FAIL: Any input that submits to nothing
❌ FAIL: Any handler that accepts input but writes nothing to DB
❌ FAIL: Any submission that gives no user feedback
```

### CHECK 2 — EVERY BUTTON DOES SOMETHING
```
List every button in this feature.
For each button state:

  Default state: [visible ✅ / invisible ❌]
  Hover state:   [styled ✅ / same as default ❌]
  Loading state: [present ✅ / missing ❌]
  Success state: [present ✅ / missing ❌]
  Error state:   [present ✅ / missing ❌]
  Disabled state:[present when needed ✅ / never disables ❌]

✅ PASS: All states designed and functional
❌ FAIL: Any button that does nothing when clicked
❌ FAIL: Any button with no loading state on async action
```

### CHECK 3 — EVERY ROUTE RETURNS SOMETHING
```
List every URL/route/endpoint in this feature.
For each:

  Route: [URL or endpoint]
  Auth: [requires login? Y/N — is it enforced?]
  Happy path: [what the user sees when it works]
  Error path: [what the user sees when it fails]
  Empty state:[what the user sees with no data]

✅ PASS: All three states handled for all routes
❌ FAIL: Any route that returns a blank page
❌ FAIL: Any route that crashes on empty data
❌ FAIL: Any protected route accessible without login
```

### CHECK 4 — EVERY ERROR IS HANDLED
```
Identify every operation that can fail in this feature:
  DB query / API call / file operation / auth check

For each:
  Error caught: [Y/N — try/catch or equivalent]
  User informed: [Y/N — what do they see]
  System logged: [Y/N — server-side log]
  Graceful: [Y/N — does the rest of the page still work]

✅ PASS: All failures caught, user informed, system logged
❌ FAIL: Any unhandled exception that crashes the page
❌ FAIL: Any silent failure (error logged but user sees nothing)
❌ FAIL: Any error that exposes system internals to user
```

### CHECK 5 — EDGE CASES IDENTIFIED AND HANDLED
```
Minimum 3 edge cases per feature. Find them.

Common edge cases to check:
  What if the user submits an empty form?
  What if the user submits the same form twice?
  What if a required related record was deleted?
  What if the user has no data yet (first-time experience)?
  What if the user has maximum data (pagination needed)?
  What if the session expires mid-action?
  What if two users do the same action simultaneously?

For this feature specifically:
  Edge case 1: [what] → [handled Y/N] → [how]
  Edge case 2: [what] → [handled Y/N] → [how]
  Edge case 3: [what] → [handled Y/N] → [how]

✅ PASS: All 3+ edge cases handled
❌ FAIL: Any identified edge case with no handler
```

### CHECK 6 — NOTIFICATIONS AND POINTS WIRED (if applicable)
```
Does this feature trigger notifications or award points
in a project that has these systems?

If YES:
  Notification sent: [Y/N — via createNotification() or equivalent]
  Points awarded:    [Y/N — via awardPoints() or equivalent]
  Points amount:     [correct value per product spec]
  Recipient:         [correct user receives notification/points]

✅ PASS: System integrations complete
❌ FAIL: Inline points update bypassing the system
❌ FAIL: Notification missing for an action that should trigger one
```

---

## GATE RESULT

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
COMPLETENESS-GATE: [Feature Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Input destinations:    ✅ / ❌
Button states:         ✅ / ❌
Route coverage:        ✅ / ❌
Error handling:        ✅ / ❌
Edge cases (3+):       ✅ / ❌
System integrations:   ✅ / ❌ / N/A

GATE: PASSED ✅ / BLOCKED ❌

[If BLOCKED]:
  Missing: [specific list]
  Complete these before UI-AGENT begins on this feature.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

*zeroslop — COMPLETENESS-GATE*

