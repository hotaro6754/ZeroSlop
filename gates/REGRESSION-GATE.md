# zeroslop — REGRESSION-GATE
> Runs after every feature is completed.
> New code must not break existing working features.

---

## What REGRESSION-GATE Does

Every new feature touches existing files.
Every file touched is a regression risk.

REGRESSION-GATE checks that nothing working
before the new feature was built is broken after it.

---

## TRIGGER

Runs after every completed feature before QA-AGENT scores.
Checks all files modified during this session.

---

## THE GATE CHECKS

### CHECK 1 — SHARED FILE IMPACT
```
List every shared file modified in this session:
  functions.php / utils.js / config.php / etc.

For each shared file modified:
  What was changed: [specific change]
  Who depends on it: [files that import/require it]
  Impact assessed: [could this change break a caller?]

For each dependent:
  [caller file]: still works with the change? [Y/N]
  If NO: [what breaks and what to fix]

✅ PASS: All dependents still work
❌ FAIL: Any dependent broken by the shared file change
```

### CHECK 2 — DB SCHEMA IMPACT
```
Was the DB schema modified in this session?
  Tables added:   [list]
  Columns added:  [list]
  Columns changed:[list] ← HIGH RISK
  Tables dropped: [list] ← CRITICAL RISK

For any column changed or dropped:
  Queries using this column: [list all files]
  Each query still valid:    [Y/N for each]
  Data migration needed:     [Y/N]

✅ PASS: No existing queries broken by schema changes
❌ FAIL: Any query now referencing a non-existent column
❌ FAIL: Any data loss without explicit migration plan
```

### CHECK 3 — AUTH SYSTEM INTEGRITY
```
Was the auth system touched in this session?

If YES:
  Change made: [what changed]
  Existing protected routes: [list all protected routes]
  Each route tested mentally: [still protected? Y/N]
  Session key changes: [any $_SESSION key renamed or removed?]
  Existing code using old session key: [list files affected]

✅ PASS: All existing auth checks still valid
❌ FAIL: Any existing protected route now broken
❌ FAIL: Any session key renamed without updating all references
```

### CHECK 4 — NAVIGATION INTEGRITY
```
Were any nav links, routes, or URLs changed?

If YES:
  Old URL: [what it was]
  New URL: [what it is now]
  All references to old URL found and updated: [Y/N]
  Any hardcoded links in other files still pointing to old URL: [Y/N]

✅ PASS: No orphan links, no 404s introduced
❌ FAIL: Any existing link now leads to a 404
❌ FAIL: Any redirect still pointing to old URL
```

### CHECK 5 — POINTS AND NOTIFICATION SYSTEM
```
If this project has a points or notification system,
and those files were touched:

  awardPoints() still works as before: [Y/N]
  createNotification() still works: [Y/N]
  Existing point values unchanged: [Y/N]
  Existing notification types unchanged: [Y/N]

✅ PASS: System integrity maintained
❌ FAIL: Any existing earned points now calculate differently
❌ FAIL: Any existing notification type broken
```

### CHECK 6 — EXISTING FEATURES SPOT CHECK
```
Name 3 existing features that were working before this session.
For each, mentally trace the full flow:

  Feature 1: [name]
    Flow: [user does X → Y happens → Z shown]
    Any file in this flow modified this session: [Y/N]
    If YES: Still works? [Y/N]

  Feature 2: [name]
    [same format]

  Feature 3: [name]
    [same format]

✅ PASS: All 3 existing features still work
❌ FAIL: Any existing feature broken by this session's changes
```

---

## GATE RESULT

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
REGRESSION-GATE: [New Feature Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Shared file impact:   ✅ / ❌
Schema impact:        ✅ / ❌ / N/A
Auth integrity:       ✅ / ❌ / N/A
Navigation integrity: ✅ / ❌ / N/A
System integrity:     ✅ / ❌ / N/A
Existing features:    ✅ / ❌

GATE: PASSED ✅ / BLOCKED ❌

[If BLOCKED]:
  Regressions found: [specific list]
  Fix before this feature is considered complete.
  A new feature that breaks old features is not a feature.
  It is technical debt shipped as progress.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

*zeroslop — REGRESSION-GATE*
