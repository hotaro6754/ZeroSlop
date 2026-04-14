# zeroslop — SECURITY-GATE
> Runs after UI-AGENT completes. Blocks handoff to QA-AGENT until every check passes.
> Security is not a final step. It is a gate every feature must pass through.

---

## What SECURITY-GATE Does

Security issues are not found at the end of a build.
They are found in every layer — DB, auth, backend, frontend.

SECURITY-GATE runs a structured audit across all layers
of every completed feature. It does not generate a report
and move on. It fixes every issue it finds before gating.

A feature with a SQL injection vector does not get a score.
It gets fixed. Then it gets a score.

---

## TRIGGER

Runs automatically after UI-AGENT gates.
Runs on every feature — not just "security-sensitive" ones.
Every feature that takes user input or touches the DB is security-sensitive.

---

## THE SECURITY AUDIT
### Ten checks. All ten. Every feature. Every time.

---

### CHECK 1 — SQL INJECTION

Every database query that uses user-supplied input must use
PDO prepared statements with bound parameters.

```
SQL INJECTION SCAN:

  Pattern to find: any query that concatenates user input
    BAD:  "SELECT * FROM users WHERE email = '" . $_POST['email'] . "'"
    BAD:  "INSERT INTO ideas VALUES ($title, $desc)"
    GOOD: $stmt = $pdo->prepare("SELECT * FROM users WHERE email = ?")
          $stmt->execute([$_POST['email']])

  Queries found: [N]
  Queries using prepared statements: [N]
  Queries with injection risk: [N] ← must be zero

  Violations fixed:
    [file] line [X]: [original] → [corrected with PDO]

RESULT: PASS ✅ / FAIL ❌
```

---

### CHECK 2 — CSRF PROTECTION

Every form that performs a state-changing action must include
and verify a CSRF token.

```
CSRF SCAN:

  Forms found that change state: [N]
  Forms with CSRF token in HTML: [N]
  Handlers that verify CSRF token: [N]
  Forms missing CSRF protection: [N] ← must be zero

  CSRF implementation check:
    Token generated per session: [Y/N]
    Token verified before processing: [Y/N]
    Token invalidated after use: [Y/N]

  Violations:
    [form in file]: missing token → [fix applied]
    [handler in file]: not verifying → [fix applied]

RESULT: PASS ✅ / FAIL ❌
```

---

### CHECK 3 — INPUT VALIDATION AND SANITIZATION

Every input from users must be validated for type and length,
and sanitized before use in any context.

```
INPUT VALIDATION SCAN:

  User inputs accepted this feature: [list them]

  For each input:
    [input_name]:
      Type validation:    [Y/N] — [what type is enforced]
      Length validation:  [Y/N] — [min/max enforced]
      Format validation:  [Y/N if applicable — email, roll_no format etc.]
      Sanitized before DB:[Y/N]
      Sanitized for HTML: [Y/N — htmlspecialchars or equivalent]
      Empty/null handled: [Y/N]

  Inputs with missing validation: [N] ← must be zero

RESULT: PASS ✅ / FAIL ❌
```

---

### CHECK 4 — CREDENTIAL AND SECRET EXPOSURE

No credentials, API keys, tokens, passwords, or secrets
in any code file.

```
CREDENTIAL SCAN:

  Files written this session: [list]

  Scanning for:
    Hardcoded DB passwords
    Hardcoded API keys
    Hardcoded tokens or secrets
    Passwords in comments
    Credentials in frontend JavaScript

  Found in code: [N] ← must be zero

  Correct pattern: all secrets in config.php or .env
  Config file is NOT committed to version control: [verified / check manually]

  Violations:
    [file] line [X]: [what was found] → moved to config

RESULT: PASS ✅ / FAIL ❌
```

---

### CHECK 5 — AUTHENTICATION ON PROTECTED ROUTES

Every route or handler that requires a logged-in user
must verify authentication before processing anything.

```
AUTH GATE SCAN:

  New routes/handlers written: [N]
  Routes that require authentication: [N]
  Routes with auth check at top: [N]
  Routes missing auth check: [N] ← must be zero

  Auth check pattern used: [matches CODEBASE-DNA pattern Y/N]

  Critical check: auth verification happens BEFORE
  any DB queries, file operations, or business logic.
  "Auth after processing" is a vulnerability.

  Violations:
    [file]: auth check missing → [fix applied]
    [file]: auth check after processing → moved to top

RESULT: PASS ✅ / FAIL ❌
```

---

### CHECK 6 — AUTHORIZATION (ROLE CHECKS)

Authentication confirms who the user is.
Authorization confirms what they are allowed to do.
Both are required.

```
AUTHORIZATION SCAN:

  Actions that require specific roles: [list them]

  For each role-restricted action:
    [action]: requires [role]
      Role check present: [Y/N]
      Role check correct: [Y/N]
      Bypass possible via URL manipulation: [Y/N] ← must be NO

  Example violation to catch:
    Admin dashboard at /admin/dashboard.php
    Checks: if($_SESSION['role'] === 'admin')
    BUT: does it redirect non-admins or just hide the UI?
    The backend handler must enforce role — not just the frontend.

  Violations:
    [file]: role check missing or bypassable → [fix applied]

RESULT: PASS ✅ / FAIL ❌
```

---

### CHECK 7 — FILE UPLOAD SECURITY (if applicable)

Only runs if this feature includes file uploads.
Skip and mark N/A if no file uploads.

```
FILE UPLOAD SCAN:

  Upload features in this build: [Y/N]
  If N/A: skip this check.

  If YES, verify:
    MIME type validated server-side (not just by extension): [Y/N]
    File extension whitelist enforced: [Y/N]
    Upload directory outside web root: [Y/N]
    Filename sanitized (no path traversal): [Y/N]
    File size limit enforced: [Y/N]
    Uploaded files cannot be executed: [Y/N]

  Violations:
    [description] → [fix applied]

RESULT: PASS ✅ / FAIL ❌ / N/A
```

---

### CHECK 8 — SENSITIVE DATA EXPOSURE

Data that should not be visible to unauthorized users
must not be accessible via direct URL or API call.

```
DATA EXPOSURE SCAN:

  Data returned by new endpoints: [list what is returned]

  Check each:
    Does response include fields the user should not see?
      e.g., password hashes, other users' private data,
      admin-only fields returned to regular users
    Is there an endpoint that returns bulk data without
      pagination or access control?
    Can a user access another user's data by changing an ID in the URL?
      e.g., /profile.php?user_id=123 — can user 456 view user 123's data?

  IDOR (Insecure Direct Object Reference) check:
    Every endpoint that accepts an ID must verify the
    requesting user has permission to access that ID.
    Not just "is logged in" — but "owns or is authorized for this record."

  Violations:
    [description] → [fix applied]

RESULT: PASS ✅ / FAIL ❌
```

---

### CHECK 9 — ERROR MESSAGE SECURITY

Error messages must not reveal system internals.

```
ERROR MESSAGE SCAN:

  Error messages shown to users in new code: [list]

  Check each:
    Does it reveal: file paths? [Y/N]
    Does it reveal: DB structure or column names? [Y/N]
    Does it reveal: stack traces? [Y/N]
    Does it reveal: server configuration? [Y/N]

  Rule: user-facing errors are always generic.
    BAD:  "PDOException: SQLSTATE[42S22]: Column not found: roll_no"
    GOOD: "Something went wrong. Please try again."

  Internal errors must be logged server-side, not displayed.

  Violations:
    [file]: [error message revealed] → replaced with generic message

RESULT: PASS ✅ / FAIL ❌
```

---

### CHECK 10 — DEPENDENCY VULNERABILITY CHECK

If new external libraries or packages were introduced,
check they are not known-vulnerable versions.

```
DEPENDENCY SCAN:

  New external dependencies introduced: [list or NONE]

  If NONE: mark PASS, skip.

  If dependencies added:
    [library name] version [X.X.X]
      Known CVEs: [check against known vulnerabilities]
      Last updated: [date — is it actively maintained?]
      Required: [why this was added]

  Recommendation: use the latest stable version.
  If a vulnerability exists: note it and recommend alternative.

RESULT: PASS ✅ / FAIL ❌ / N/A
```

---

## SECURITY GATE REPORT

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SECURITY-GATE REPORT
Feature: [name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CHECK RESULTS:
  SQL Injection:        PASS ✅ / FAIL ❌
  CSRF Protection:      PASS ✅ / FAIL ❌
  Input Validation:     PASS ✅ / FAIL ❌
  Credential Exposure:  PASS ✅ / FAIL ❌
  Authentication:       PASS ✅ / FAIL ❌
  Authorization:        PASS ✅ / FAIL ❌
  File Upload:          PASS ✅ / FAIL ❌ / N/A
  Data Exposure/IDOR:   PASS ✅ / FAIL ❌
  Error Messages:       PASS ✅ / FAIL ❌
  Dependencies:         PASS ✅ / FAIL ❌ / N/A

Issues found and fixed: [N]
Issues found and deferred (with reason): [N]

GATE RESULT: PASSED ✅ / BLOCKED ❌

[If PASSED]: Handing off to QA-AGENT.
[If BLOCKED]: 
  Cannot proceed. Security issues are not optional.
  Remaining issues: [list]
  These must be fixed before QA-AGENT begins.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## NON-NEGOTIABLES

```
These checks NEVER get deferred. They NEVER get "noted for later."
They are fixed before the gate passes. No exceptions.

  ⛔ SQL injection vulnerability
  ⛔ Missing CSRF on state-changing form
  ⛔ Hardcoded credentials in any file
  ⛔ Protected route with no auth check
  ⛔ IDOR vulnerability on any user-owned resource
```

Everything else can be discussed. These five cannot.

---

*zeroslop — SECURITY-GATE*
*Part of the zeroslop methodology: github.com/harshithgangaraju/zeroslop*
