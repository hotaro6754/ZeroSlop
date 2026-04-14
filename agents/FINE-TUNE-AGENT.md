# zeroslop — FINE-TUNE-AGENT
> The last agent in the pipeline. Only runs in GROUNDED MODE.
> This is the 1000x protocol. This is what makes zeroslop different from everything else.

---

## What FINE-TUNE-AGENT Does

Every other agent builds features.
FINE-TUNE-AGENT makes those features feel like they were always there.

Without FINE-TUNE-AGENT, new code is technically correct but foreign.
It uses slightly different naming. It handles errors differently.
It reinvents utilities that already exist. It connects to systems
in a slightly different way than everything else does.

The codebase feels like it was built by three different people.
Because without FINE-TUNE-AGENT, it was.

FINE-TUNE-AGENT reads CODEBASE-DNA and runs a surgical
consistency pass on everything built in this session.
After it runs, the new code is indistinguishable from
code that has been in the project for months.

That is the 1000x.

---

## TRIGGER CONDITIONS

FINE-TUNE-AGENT activates:
```
✅ After QA-AGENT gates (all features score 70+)
✅ ONLY when GROUNDED MODE is active (COLD-READ has run)
✅ After every feature in a long session — not just at the end
```

FINE-TUNE-AGENT does NOT activate:
```
❌ If COLD-READ has not run (no CODEBASE-DNA to match against)
❌ Before QA-AGENT gates
❌ On its own layer — it reviews and fixes, never builds new features
```

If GROUNDED MODE is not active:
Tell the user: "FINE-TUNE-AGENT requires your codebase.
Paste your repo or key files to activate GROUNDED MODE
and unlock the full fine-tune pass."

---

## THE FINE-TUNE PROTOCOL
### Eight consistency checks. Run all eight. Fix every failure found.

---

### CHECK 1 — UTILITY DUPLICATION SCAN

Cross-reference every function written in this session
against the UTILITIES INVENTORY from COLD-READ.

Ask for every new function written:
```
Does a function that does this already exist in the codebase?

If YES:
  → Delete the new function
  → Replace all calls with the existing utility
  → State: "REPLACED: [new_function()] with existing [utility()]
            from [file]. Reason: duplicate logic."

If NO:
  → The new function belongs
  → Consider: should it be added to the shared utilities file?
  → If yes: move it there and update all references
```

Report:
```
UTILITY SCAN:
  New functions written this session: [N]
  Duplicates found and replaced: [N]
    - [new_function()] → replaced with [existing_utility()]
    - [new_function()] → replaced with [existing_utility()]
  New utilities added to shared file: [N]
    - [function()] added to [functions.php / utils.js / etc.]
```

---

### CHECK 2 — NAMING CONVENTION ENFORCEMENT

Every variable, function, file, and DB column written this session
must match the conventions locked in CODEBASE-DNA.

```
CONVENTION AUDIT:
  
  Expected naming (from COLD-READ):
    Functions:   [camelCase / snake_case]
    Variables:   [camelCase / snake_case / $prefix]
    Files:       [kebab-case / snake_case]
    DB columns:  [snake_case / camelCase]
  
  Violations found:
    [filename] line [X]: [what was written] → should be [correct form]
    [filename] line [X]: [what was written] → should be [correct form]
  
  Violations fixed: [N]
  Violations remaining: 0 (must be zero to gate)
```

Zero tolerance. One naming violation breaks the consistency of
the entire codebase. Fix every single one.

---

### CHECK 3 — AUTH PATTERN CONSISTENCY

Every protected route and action written this session must use
the exact same auth check method as the rest of the codebase.

```
AUTH CONSISTENCY AUDIT:

  Auth pattern from COLD-READ:
    Method:       [e.g., session check in auth_check.php]
    Session key:  [e.g., $_SESSION['roll_no']]
    Role check:   [e.g., $_SESSION['role'] === 'visionary']
  
  New protected routes written: [N]
  Routes using correct auth method: [N]
  Routes using incorrect/custom auth: [N]
  
  Violations found:
    [filename]: [what was written] → [what it should be]
  
  All violations fixed: YES / NO
```

A new auth pattern introduced by this session is a security risk.
It creates a code path that may not be maintained or updated correctly.
Every protected route must use the established pattern.

---

### CHECK 4 — ERROR HANDLING CONSISTENCY

Every new handler must handle errors the same way
existing handlers do.

```
ERROR HANDLING AUDIT:

  Error pattern from COLD-READ:
    [e.g., try/catch → JSON response with 'error' key]
    [e.g., die() with custom message]
    [e.g., custom handleError() function]
  
  New handlers written: [N]
  Handlers using correct error pattern: [N]
  Handlers with custom/missing error handling: [N]
  
  Violations found:
    [filename]: [what was written] → [what it should be]
  
  All violations fixed: YES / NO
```

---

### CHECK 5 — SYSTEM INTEGRATION CHECK

Does new code connect to existing systems correctly?

Check each of the following that exists in CODEBASE-DNA:

```
POINTS SYSTEM:
  If project has awardPoints() or similar:
  → Every action that should award points MUST call awardPoints()
  → No inline points manipulation (e.g., direct UPDATE to points column)
  
  New point-awarding actions: [N]
  Actions using awardPoints(): [N]
  Actions with inline points: [N] ← must be zero
  
NOTIFICATIONS SYSTEM:
  If project has createNotification() or similar:
  → Every action that should notify MUST call createNotification()
  → No custom notification logic inline in handlers
  
  New notification triggers: [N]
  Triggers using createNotification(): [N]
  Triggers with inline notification: [N] ← must be zero

LOGGING SYSTEM (if exists):
  → All significant actions logged using existing log function
  → No custom logging implemented inline

AUDIT:
  Points system compliance:        ✅ / ❌
  Notifications system compliance: ✅ / ❌
  Logging system compliance:       ✅ / N/A
```

---

### CHECK 6 — RESPONSE FORMAT CONSISTENCY

Every handler must return responses in the same format
as existing handlers.

```
RESPONSE FORMAT AUDIT:

  Response format from COLD-READ:
    Success: [e.g., {"status": "success", "data": {...}}]
    Error:   [e.g., {"status": "error", "message": "..."}]
    Redirect:[e.g., header("Location: /dashboard.php")]
  
  New handlers written: [N]
  Using correct success format: [N]
  Using correct error format: [N]
  Using non-standard format: [N]
  
  Violations:
    [filename]: returns [what] → should return [correct format]
  
  All violations fixed: YES / NO
```

---

### CHECK 7 — PERFORMANCE QUICK SCAN

Check for common performance issues introduced by new code.

```
PERFORMANCE SCAN:

  N+1 QUERIES:
    Any loop that runs a DB query inside it?
    [filename] line [X]: [description of N+1 pattern]
    Fix: [how to resolve — JOIN, eager load, collect IDs first]

  MISSING INDEXES:
    Any column being queried in WHERE/ORDER BY/JOIN that 
    has no index in the schema?
    [table.column]: no index → ADD INDEX recommendation

  UNBOUNDED QUERIES:
    Any SELECT with no LIMIT in a context where the result 
    set could grow large?
    [filename] line [X]: [description] → add LIMIT [N]

  REPEATED QUERIES:
    Any query that runs the same thing multiple times 
    in one request that could be cached or batched?
    [filename]: [description] → [optimization]

  Performance issues found: [N]
  Performance issues fixed: [N]
  Performance issues deferred (with reason): [N]
```

---

### CHECK 8 — DEAD CODE SCAN

Did this session introduce any new dead code?

```
DEAD CODE SCAN:

  Functions defined but never called: [N]
    [function name] in [file] — [action: remove / keep with reason]

  Variables declared but never used: [N]
    [variable] in [file] line [X] — removed

  Commented-out code blocks (5+ lines): [N]
    [file] lines [X-Y] — [action: remove / document why kept]

  Files created but never imported/required: [N]
    [filename] — [action: connect or remove]

  Dead code introduced this session: [N]
  Dead code removed: [N]
```

---

## FINE-TUNE REPORT

After all eight checks, produce this report:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FINE-TUNE-AGENT REPORT
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Feature tuned: [feature name]
GROUNDED MODE: ACTIVE — matched against [N] existing files

CHECK RESULTS:
  ✅ Utility duplication:      [N duplicates removed]
  ✅ Naming conventions:       [N violations fixed]
  ✅ Auth consistency:         [N routes corrected]
  ✅ Error handling:           [N handlers corrected]
  ✅ System integration:       [points/notifications verified]
  ✅ Response format:          [N responses corrected]
  ✅ Performance:              [N issues addressed]
  ✅ Dead code:                [N items removed]

CHANGES MADE THIS PASS:
  [file]: [what changed and why]
  [file]: [what changed and why]
  [file]: [what changed and why]

GATE CONDITIONS:
  □ Zero utility duplicates
  □ Zero naming violations
  □ Zero auth pattern deviations
  □ Zero system integration bypasses
  □ Zero response format inconsistencies
  □ No unaddressed performance issues

GATE RESULT: PASSED ✅ / FAILED ❌

[If PASSED]:
  This feature is now indistinguishable from 
  code that has been in this project for months.
  Build complete.

[If FAILED]:
  [Specific remaining issues]
  Rerunning affected checks.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## THE 1000X COMPARISON

Without FINE-TUNE-AGENT:
```
New feature added to IdeaSync:
  → Uses getDbConnection() (invented — existing is getDB())
  → Awards points with: UPDATE users SET points = points + 10
    (existing system uses awardPoints() — points_log has no record)
  → Returns {"success": true} 
    (existing format is {"status": "success"} — frontend breaks)
  → Session check: if($_SESSION['user_id']) 
    (existing uses $_SESSION['roll_no'] — always fails)
  
  Result: Feature is technically complete.
          Nothing in it actually works with the real codebase.
```

With FINE-TUNE-AGENT:
```
New feature added to IdeaSync:
  → Uses getDB() — matched from CODEBASE-DNA
  → Awards points via awardPoints($userId, 10, 'idea_posted')
    — points_log has the record, leaderboard updates correctly
  → Returns {"status": "success", "data": {...}}
    — frontend receives expected format, renders correctly
  → Session check: if(!isset($_SESSION['roll_no'])) redirect to login
    — matches every other protected page exactly
  
  Result: Feature works. Fits perfectly. Ships.
```

That gap is why FINE-TUNE-AGENT exists.
That gap is the entire value of GROUNDED MODE.

---

*zeroslop — FINE-TUNE-AGENT*
*Part of the zeroslop methodology: github.com/hotaro6754/ZeroSlop*

