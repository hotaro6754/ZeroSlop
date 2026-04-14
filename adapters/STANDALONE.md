# zeroslop — ADAPTER: WITH-SUPERPOWERS
> Use zeroslop on top of superpowers (obra/superpowers).
> zeroslop adds intelligence gates after each superpowers skill.

---

## How They Work Together

```
superpowers handles:  TDD methodology, skill-based agents,
                      test-first development, subagent workflow

zeroslop adds:        Pre-build market intelligence (SCOUT)
                      Design intelligence (DESIGN-SCOUT)
                      Post-skill quality gates
                      Self-scoring with rebuild enforcement
                      Codebase DNA grounding
```

superpowers ensures features are test-driven.
zeroslop ensures the features being built are the right ones,
built with the right design, and scored honestly.

---

## Workflow: superpowers + zeroslop

```
BEFORE superpowers starts any skill:
  1. Run zeroslop SCOUT + VALIDATE on the feature
  2. Run zeroslop COLD-READ if repo not already loaded
  3. Run zeroslop DESIGN-SCOUT before any UI skill

DURING superpowers skill execution:
  superpowers runs as normal — TDD, test-first, subagents

AFTER each superpowers skill completes:
  Run the appropriate zeroslop gate:
    After a backend skill  → COMPLETENESS-GATE + SECURITY-GATE
    After a frontend skill → DESIGN-GATE
    After any skill        → QA-AGENT self-score
    
  If score < 70: tell superpowers to redo the skill
  If score ≥ 70: proceed to next skill
```

---

## The Gate Insert

After any superpowers skill response, immediately run:

```
"Using zeroslop QA-AGENT, score what was just built.
 Apply the self-score rubric from BOOT.md.
 If score is below 70, rebuild the skill output.
 Do not proceed to the next skill until score ≥ 70."
```

---

*zeroslop — Adapter: WITH-SUPERPOWERS*

---
---

# zeroslop — ADAPTER: STANDALONE
> No other tools needed. zeroslop works completely on its own.
> This is the default mode for most users.

---

## Who This Is For

```
✅ You don't use Cursor, GSD, or superpowers
✅ You work directly with Claude, GPT-4, or Gemini
✅ You paste files into the chat directly
✅ You want the full zeroslop pipeline without setup
```

---

## Standalone Setup (30 seconds)

```
Option A — Minimum viable (just BOOT.md):
  1. Open a new AI session
  2. Paste the full content of BOOT.md
  3. AI confirms zeroslop loaded
  4. Paste your codebase or idea
  5. Pipeline runs automatically

Option B — Full pipeline (all core files):
  1. Open a new AI session
  2. Paste BOOT.md
  3. Paste 01-COLD-READ.md (if you have a codebase)
  4. Paste 02-SCOUT.md + 02b-DESIGN-SCOUT.md
  5. Paste the 4 gate files
  6. Paste your profile (saas / campus / fintech / healthcare)
  7. Paste your codebase or idea
  8. Full pipeline runs

Option C — Modular (add as needed):
  Start with BOOT.md.
  Add specific files when their stage activates.
  Don't need DESIGN-SCOUT? Don't paste it.
  zeroslop works with whatever is loaded.
```

---

## Standalone Session Template

Copy this at the start of every session:

```
I'm loading the zeroslop methodology for this session.
[paste BOOT.md content here]

[if codebase]: Here is my project:
[paste files here]

[if new idea]: Here is what I want to build:
[paste PRD/README/description here]
```

---

## Standalone Tips

```
ONE SESSION = ONE FEATURE (recommended)
  Don't try to build an entire app in one session.
  Load zeroslop. Build one feature. Gate it. Score it.
  New session for the next feature with updated codebase.

PASTE CODEBASE-DNA ACROSS SESSIONS
  After COLD-READ generates CODEBASE-DNA,
  save that output. Paste it into every new session.
  This preserves GROUNDED MODE across sessions without
  repasting the entire codebase.

UPDATE CODEBASE-DNA WHEN SCHEMA CHANGES
  After DB-AGENT adds new tables,
  update your saved CODEBASE-DNA with the new schema.
  Next session will be grounded to the current state.
```

---

*zeroslop — Adapter: STANDALONE*
