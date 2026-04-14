# zeroslop — 03-VALIDATE
> Activates after SCOUT completes, before any architecture or build begins.
> This is the truth protocol. SCOUT finds the data. VALIDATE interprets it.

---

## What VALIDATE Does

SCOUT returns raw market data.
VALIDATE turns that data into a decision.

VALIDATE answers three questions with evidence — not opinion:

1. Is the problem real and worth solving?
2. Is this approach genuinely different from what exists?
3. What specifically needs to be true for this to win?

If you cannot answer all three with evidence from SCOUT data,
VALIDATE sends you back to SCOUT for more research.
You do not move forward on a hunch.

---

## TRIGGER CONDITIONS

VALIDATE activates:
```
✅ Automatically after SCOUT completes
✅ When user provides SCOUT data and asks to proceed
✅ When user says "validate my idea" with prior context
```

VALIDATE requires SCOUT data to run.
If SCOUT has not been run, do not guess.
Say: "SCOUT must run first. Paste your idea and I will begin research."

---

## THE VALIDATE PROTOCOL
### Five validation checks. All five must pass before proceeding.

---

### VALIDATION CHECK 1 — PROBLEM REALITY TEST

The problem being solved must be documented by real users.
Not assumed. Not theorized. Documented.

Evidence sources (from SCOUT TARGET 3):
- Reddit complaints
- HackerNews threads
- ProductHunt negative comments
- App store reviews of competitors
- Any public forum where users expressed this pain

Run this test:
```
PROBLEM REALITY TEST:
  Problem stated:     [what the user says the problem is]
  Evidence found:     [specific sources from SCOUT data]
  People affected:    [how many — approximate from sources]
  
  Current solutions:  [how people solve this today]
  Why current solutions fail: [specific documented reasons]
  
  RESULT: REAL ✅ / ASSUMED ❌ / WEAK ⚠
```

REAL: Multiple independent sources document this pain.
ASSUMED: No external evidence found. User believes it is a problem.
WEAK: One or two mentions. Not enough signal.

If RESULT is ASSUMED or WEAK:
Do not proceed. Tell the user exactly what evidence is missing.
Tell them where to look before VALIDATE can pass.

---

### VALIDATION CHECK 2 — SOLUTION DIFFERENTIATION TEST

Compare the proposed solution against every competitor from SCOUT TARGET 1
and every OSS alternative from SCOUT TARGET 2.

This is not about whether the idea is good.
This is about whether the idea is different.

Run this test:
```
DIFFERENTIATION TEST:

For each competitor [A, B, C...]:

  [Competitor A]:
    What they do:      [core functionality]
    What they do well: [strengths]
    What they miss:    [gaps from SCOUT TARGET 3 pain points]
    Overlap with idea: [%] of proposed features already exist here

  [Competitor B]:
    ...

OVERLAP SUMMARY:
  Average feature overlap with existing solutions: [%]
  Features that are completely unique to this idea: [list them]
  Features that partially overlap but could be done better: [list them]
  Features that are fully covered by competitors: [list them]

DIFFERENTIATION SCORE: __/100
```

Scoring guide:
```
90-100: Nearly all features are genuinely new. Rare. Proceed with confidence.
70-89:  Strong differentiation. 2-3 clear unique features. Proceed.
50-69:  Moderate overlap. Must double down on the unique features.
        State which features are the moat. Build those first.
30-49:  High overlap. The idea needs a clear pivot or sharper angle.
        Do not proceed until pivot is defined.
0-29:   This is a clone. Building it as-is is not recommended.
        Identify the 1 thing that could make it different and pivot hard.
```

---

### VALIDATION CHECK 3 — MOAT IDENTIFICATION

The moat is the reason someone would use this instead of existing solutions.
It must be specific. "Better UX" is not a moat. "More features" is not a moat.

A real moat is one of these:
```
TYPE A — UNIQUE FEATURE MOAT
  Something this product does that literally nobody else does.
  Example: "Permanent archive of student projects that survives graduation"

TYPE B — AUDIENCE MOAT
  Built for a specific audience that existing tools ignore.
  Example: "Built specifically for Indian engineering college campuses
           with roll number auth and batch/branch systems"

TYPE C — INTEGRATION MOAT
  Combines things that exist separately in a way nobody has done.
  Example: "GitHub activity + gamification + campus leaderboard in one system"

TYPE D — DISTRIBUTION MOAT
  Access to an audience that competitors cannot easily reach.
  Example: "Direct access to Lendi campus — 3000 students day one"

TYPE E — TRUST MOAT
  Built by someone the audience trusts more than a generic product.
  Example: "Built by a Lendi student, for Lendi students"
```

Run this test:
```
MOAT IDENTIFICATION:
  Moat type:      [A / B / C / D / E — can be multiple]
  Moat statement: [one sentence — specific and defensible]
  
  Why competitors haven't built this:
    [Reason 1 — e.g., "Too niche for their market"]
    [Reason 2 — e.g., "Requires campus-specific integration"]
    
  How long until a competitor could copy this:
    [SHORT (weeks) / MEDIUM (months) / LONG (years or structural)]
    
  What makes the moat defensible over time:
    [e.g., "Network effects — more students = more valuable archive"]

MOAT RESULT: STRONG ✅ / EXISTS ⚠ / WEAK ❌ / MISSING ❌
```

If MOAT RESULT is WEAK or MISSING:
Stop. Do not proceed to INTERROGATE.
The user is about to build something they cannot defend.
Tell them directly and help them identify a real moat first.

---

### VALIDATION CHECK 4 — TIMING TEST

Is this the right time to build this?

```
TIMING TEST:
  Market trend:       GROWING / STABLE / DECLINING
  Evidence:           [from SCOUT TARGET 5 recent launches]
  
  Recent launches in space: [N in last 6 months]
  Interpretation:
    0 recent launches:  Space may be untapped OR abandoned
    1-3 recent launches: Healthy signal. Market is active.
    4+ recent launches:  Market is heating up — move fast OR find a niche
  
  Technology readiness:
    Are the APIs and tools needed to build this mature?
    [YES — everything needed exists and is stable]
    [PARTIAL — some dependencies are immature or expensive]
    [NO — key infrastructure doesn't exist yet]
    
  User readiness:
    Is the target audience ready to adopt this?
    [e.g., "College students already use GitHub — low adoption friction"]
    
TIMING RESULT: GOOD ✅ / EARLY ⚠ / LATE ❌
```

GOOD: Market is growing, tools are ready, audience is ready.
EARLY: The idea is right but the market hasn't caught up yet.
LATE: Well-funded competitors have already captured this space.

---

### VALIDATION CHECK 5 — BUILD VS BUY TEST

Before recommending a full build, check:
can the user achieve their goal faster by combining existing tools?

```
BUILD VS BUY TEST:
  Could this be achieved with:
    Existing no-code tools:  YES / NO / PARTIAL
    Combining existing APIs: YES / NO / PARTIAL
    Forking an OSS project:  YES / NO / PARTIAL
    
  If partial or yes — state specifically what could be reused:
    [e.g., "Authentication could use Supabase instead of custom PHP"]
    [e.g., "GitHub integration already handled by [existing library]"]
    
  Build recommendation:
    BUILD FROM SCRATCH: [reason — usually unique architecture needed]
    HYBRID: Build [X] custom, use [Y] existing tools for [Z]
    FORK AND EXTEND: [specific OSS repo] covers 60% — extend it
```

This is not about laziness. It is about shipping faster.
A hybrid approach that ships in 2 weeks beats a custom build
that ships in 3 months — especially for an MVP.

---

## VALIDATE FINAL REPORT

After all five checks, produce this block:

```
╔══════════════════════════════════════════════════════╗
║  ZEROSLOP VALIDATION REPORT                         ║
╠══════════════════════════════════════════════════════╣
║  Idea:              [one line]                      ║
╠══════════════════════════════════════════════════════╣
║  FIVE CHECK RESULTS                                 ║
║  Problem Reality:       REAL ✅ / ASSUMED ❌ / WEAK ⚠ ║
║  Differentiation:       __/100                      ║
║  Moat:                  STRONG ✅ / EXISTS ⚠ / WEAK ❌║
║  Timing:                GOOD ✅ / EARLY ⚠ / LATE ❌  ║
║  Build vs Buy:          [recommendation]            ║
╠══════════════════════════════════════════════════════╣
║  VALIDATION SCORE:      __/100                      ║
║                                                     ║
║  Scoring:                                           ║
║  Problem Reality (25pts): __/25                     ║
║  Differentiation (25pts): __/25                     ║
║  Moat strength (25pts):   __/25                     ║
║  Timing (15pts):          __/15                     ║
║  Build efficiency (10pts):__/10                     ║
╠══════════════════════════════════════════════════════╣
║  KEY RISKS                                          ║
║  ⚠ [specific risk 1 with mitigation]               ║
║  ⚠ [specific risk 2 with mitigation]               ║
║  ⚠ [specific risk 3 with mitigation]               ║
╠══════════════════════════════════════════════════════╣
║  THE ONE SENTENCE PITCH                             ║
║  (Synthesized from moat + pain points)              ║
║  "[Product] is the only [category] that [moat]     ║
║   for [specific audience] who [specific pain]"     ║
╠══════════════════════════════════════════════════════╣
║  FINAL VERDICT                                      ║
║  [BUILD / BUILD WITH CHANGES / PIVOT / STOP]       ║
║                                                     ║
║  If BUILD:             Proceed to INTERROGATE       ║
║  If BUILD WITH CHANGES:[state exactly what changes] ║
║  If PIVOT:             [state exactly what to pivot]║
║  If STOP:              [state exactly why + options]║
╚══════════════════════════════════════════════════════╝
```

---

## VERDICT BEHAVIOR

**BUILD (80-100):**
All checks pass. Moat is clear. Problem is real. Proceed to STAGE 4 — INTERROGATE.

**BUILD WITH CHANGES (60-79):**
Good foundation but specific things need to change.
State exactly what must change. Get user confirmation.
Do not proceed to INTERROGATE until changes are agreed.

**PIVOT (35-59):**
The idea has a real problem at its core but the approach needs work.
Give the user 2-3 specific pivot directions with reasoning.
Let them choose. Rerun VALIDATE on the pivot before proceeding.

**STOP (0-34):**
Be direct. Something fundamental is broken:
- The problem isn't real
- A dominant competitor already owns this space
- The moat doesn't exist
State exactly what was found. Suggest what to explore instead.

---

## WHAT VALIDATE DOES NOT DO

```
❌ Does not validate business models or financial projections
❌ Does not guarantee success
❌ Does not soften findings to protect the user's feelings
❌ Does not skip checks because the user seems excited
❌ Does not change its verdict because the user pushes back
   (If new evidence is provided, rerun the check. If not — verdict stands.)
```

---

## VALIDATE → INTERROGATE HANDOFF

When VALIDATE returns BUILD or BUILD WITH CHANGES (agreed),
automatically transition to STAGE 4 — INTERROGATE.

Tell the user:
```
VALIDATION COMPLETE.

Score: [X]/100 — [BUILD / BUILD WITH CHANGES]
Moat confirmed: [one line moat statement]

Moving to INTERROGATE.
I have [N] questions before architecture begins.
These are the only things I could not determine from
your idea and the market data. Answers change real files.
```

---

*zeroslop — 03-VALIDATE*
*Part of the zeroslop methodology: github.com/harshithgangaraju/zeroslop*
