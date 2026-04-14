# zeroslop — 05-RATE
> Activates after INTERROGATE completes.
> This is the reality check protocol. You know exactly what you're walking into before line one.

---

## What RATE Does

After SCOUT, VALIDATE, and INTERROGATE —
you have a complete picture of the idea and all architecture decisions.

RATE takes that picture and produces an honest assessment:
- How complex is this actually?
- Where will it break?
- What should be built in Phase 1 vs later?
- What is the real estimated effort?

No surprises mid-build.
No "I didn't realize this would be so complex" at week three.
RATE makes the invisible visible before the first file is created.

---

## TRIGGER CONDITIONS

RATE activates:
```
✅ Automatically after INTERROGATE completes
✅ When user provides a complete feature spec with all decisions made
✅ When user says "rate this requirement" with full context available
```

RATE requires:
```
- VALIDATE findings (problem is real, moat is identified)
- INTERROGATE answers (all architecture decisions locked)
- CODEBASE-DNA if GROUNDED MODE is active
```

If any of the above are missing, state what is needed before RATE can run.

---

## THE RATE PROTOCOL
### Six scoring dimensions. All six produce the final REQUIREMENT RATING.

---

### DIMENSION 1 — CLARITY SCORE (25 points)

Is the requirement precise enough to build without guessing?

```
CLARITY ASSESSMENT:

  Is the core feature completely defined?         [Y/N] — [X] pts
  Are all user roles and permissions defined?     [Y/N] — [X] pts
  Are all data relationships defined?             [Y/N] — [X] pts
  Are all edge cases identified?                  [Y/N] — [X] pts
  Are success criteria defined?                   [Y/N] — [X] pts

  CLARITY SCORE: __/25

  Open ambiguities remaining (if any):
    - [ambiguity 1 — what is still unclear]
    - [ambiguity 2]
```

If CLARITY SCORE < 15:
Stop. Do not proceed to build.
The requirement is too vague to execute without major mid-build changes.
Return to INTERROGATE with the specific ambiguities listed.

---

### DIMENSION 2 — FEASIBILITY SCORE (25 points)

Can this actually be built with the stated constraints?

```
FEASIBILITY ASSESSMENT:

  Tech stack constraints:
    Is the chosen stack capable of all required features? [Y/N]
    Are there known limitations? [list them]

  External dependency feasibility:
    Are all required APIs available and within budget?    [Y/N]
    Are there rate limits that could break features?      [Y/N — flag if yes]
    Are there third-party terms of service risks?         [Y/N — flag if yes]

  Hosting feasibility:
    Can the hosting environment support all features?     [Y/N]
    Are there features requiring infra the user doesn't have? [Y/N]

  Time feasibility:
    Is the scope achievable in the user's stated timeline? [Y/N]
    If no timeline stated — estimate honestly.

  FEASIBILITY SCORE: __/25

  Blockers (if any):
    ⛔ [blocker 1 — what specifically cannot be built as stated]
    ⛔ [blocker 2]

  Constraints (risks but not blockers):
    ⚠ [constraint 1 — e.g., GitHub API rate limits at scale]
    ⚠ [constraint 2]
```

If there are ⛔ BLOCKERS:
Do not proceed. These must be resolved.
A blocker is not a risk. It is something that cannot be built as specified.
Offer concrete resolution paths. Do not just list the problem.

---

### DIMENSION 3 — COMPLEXITY SCORE (20 points)

How complex is this relative to a standard feature?

```
COMPLEXITY ASSESSMENT:

  DB complexity:
    Tables needed:              [N]
    Relationships (FK links):   [N]
    Pivot tables needed:        [N]
    Migrations needed:          [N]
    
    DB Complexity:  LOW (1-3 tables) / 
                    MEDIUM (4-8 tables) / 
                    HIGH (9+ tables or complex relations)

  Backend complexity:
    Handlers/endpoints needed:  [N]
    Business logic files:       [N]
    External API integrations:  [N]
    Background jobs needed:     [Y/N]
    
    Backend Complexity: LOW / MEDIUM / HIGH

  Frontend complexity:
    Pages/views needed:         [N]
    Components needed:          [N]
    Real-time elements:         [Y/N]
    Chart/data viz needed:      [Y/N]
    
    Frontend Complexity: LOW / MEDIUM / HIGH

  Auth complexity:
    New roles needed:           [N]
    Permission rules needed:    [N]
    
    Auth Complexity: LOW / MEDIUM / HIGH

  COMPLEXITY SCORE: __/20
  Overall complexity: LOW / MEDIUM / HIGH / VERY HIGH
```

Complexity score is not about penalizing complexity.
HIGH complexity gets a HIGH score if it is ACCURATE.
A wrong complexity assessment — either under or over — scores low.

---

### DIMENSION 4 — RISK SCORE (15 points)

What can go wrong and how badly?

```
RISK ASSESSMENT:

  TECHNICAL RISKS:
    ⚠ [risk] — Probability: LOW/MED/HIGH — Impact: LOW/MED/HIGH
    ⚠ [risk] — Probability: LOW/MED/HIGH — Impact: LOW/MED/HIGH

  SCOPE RISKS:
    ⚠ [risk — e.g., "5 user roles creates 5x auth edge cases"]
    ⚠ [risk — e.g., "Gamification invites point manipulation"]

  DEPENDENCY RISKS:
    ⚠ [risk — e.g., "GitHub API: 60 req/hr unauthenticated"]
    ⚠ [risk — e.g., "Email delivery requires third-party service"]

  TIMELINE RISKS:
    ⚠ [risk — e.g., "Estimated 3 weeks, stated deadline is 1 week"]

  For each HIGH probability + HIGH impact risk:
    Mitigation: [specific, actionable mitigation step]

  RISK SCORE: __/15
  (High score = risks are identified and mitigated, not that there are no risks)
```

---

### DIMENSION 5 — PHASE RECOMMENDATION (10 points)

What should actually be built in Phase 1?

```
PHASE ANALYSIS:

  MUST HAVE (Phase 1 — without this, the product doesn't work):
    ✅ [feature]
    ✅ [feature]
    ✅ [feature]

  SHOULD HAVE (Phase 1 — adds significant value, manageable scope):
    ⚡ [feature]
    ⚡ [feature]

  NICE TO HAVE (Phase 2 — valuable but not launch-blocking):
    💡 [feature]
    💡 [feature]

  DEFER (Phase 3+ — complex, risky, or premature):
    ⏳ [feature]
    ⏳ [feature]

  Phase 1 scope impact:
    Files:    ~[N]
    Tables:   ~[N]
    Effort:   ~[N] hours / days

  PHASE SCORE: __/10
  (High score = recommendation is realistic and well-reasoned)
```

---

### DIMENSION 6 — GROUNDED MODE BONUS (5 points)

Only applies if COLD-READ has run and GROUNDED MODE is active.

```
GROUNDED MODE ASSESSMENT:

  Utilities available that reduce build time:
    ✅ [utility] handles [what] — saves ~[X] hrs
    ✅ [utility] handles [what] — saves ~[X] hrs

  Existing patterns that can be reused:
    ✅ [pattern] — no new code needed for [what]

  Dead zones that must be fixed before this build:
    ⚠ [dead zone] — must fix first or this feature breaks

  Net build time reduction from GROUNDED MODE: ~[X] hrs

  GROUNDED BONUS: __/5
```

---

## THE REQUIREMENT RATING BLOCK

After all six dimensions, produce the final rating:

```
╔══════════════════════════════════════════════════════════╗
║  ZEROSLOP REQUIREMENT RATING                            ║
╠══════════════════════════════════════════════════════════╣
║  Project:    [name]                                     ║
║  Feature:    [what is being rated]                      ║
╠══════════════════════════════════════════════════════════╣
║  DIMENSION SCORES                                       ║
║  Clarity:        __/25  [one line assessment]           ║
║  Feasibility:    __/25  [one line assessment]           ║
║  Complexity:     __/20  [LOW/MEDIUM/HIGH/VERY HIGH]     ║
║  Risk:           __/15  [one line assessment]           ║
║  Phase Plan:     __/10  [one line assessment]           ║
║  Grounded Bonus: __/5   [N/A if no COLD-READ]          ║
╠══════════════════════════════════════════════════════════╣
║  TOTAL SCORE:    __/100                                 ║
╠══════════════════════════════════════════════════════════╣
║  SCOPE SUMMARY                                          ║
║  Phase 1 files:    ~__                                  ║
║  Phase 1 tables:   ~__                                  ║
║  Phase 1 effort:   ~__ hours / ~__ days                 ║
║  External APIs:    __                                   ║
╠══════════════════════════════════════════════════════════╣
║  TOP 3 RISKS                                            ║
║  ⚠ [risk 1 + mitigation in one line]                   ║
║  ⚠ [risk 2 + mitigation in one line]                   ║
║  ⚠ [risk 3 + mitigation in one line]                   ║
╠══════════════════════════════════════════════════════════╣
║  BLOCKERS (must resolve before build)                   ║
║  ⛔ [blocker 1] — OR — None                             ║
╠══════════════════════════════════════════════════════════╣
║  BUILD RECOMMENDATION                                   ║
║  [PROCEED / PROCEED WITH CAUTION / RESOLVE FIRST]      ║
║                                                         ║
║  Phase 1 focus: [what to build first in one line]      ║
╚══════════════════════════════════════════════════════════╝
```

---

## RATING THRESHOLDS

```
85-100: PROCEED
  Requirement is clear, feasible, risks are known and managed.
  Move to ORCHESTRATE immediately.

70-84: PROCEED WITH CAUTION
  Good foundation. Named risks need active monitoring.
  State which risks to watch during build.
  Move to ORCHESTRATE but flag the risks to revisit after each agent.

50-69: RESOLVE FIRST
  Specific problems exist. List them. Fix them.
  Do not move to ORCHESTRATE until score improves.
  What needs to change to reach 70+: [specific list]

Below 50: STOP AND REDESIGN
  The requirement has fundamental problems.
  Do not build. Redesign the approach.
  Identify the 2-3 root causes of the low score and address them.
```

---

## RATE → ORCHESTRATE HANDOFF

When score is 70+ and no blockers exist:
Automatically transition to STAGE 6 — ORCHESTRATE.

Tell the user:
```
RATE COMPLETE.

Score: [X]/100 — [PROCEED / PROCEED WITH CAUTION]
Phase 1 scope locked: ~[N] files, ~[N] tables, ~[N] days

Moving to ORCHESTRATE.
Breaking work into agents with dependencies and gates.
```

---

*zeroslop — 05-RATE*
*Part of the zeroslop methodology: github.com/harshithgangaraju/zeroslop*
