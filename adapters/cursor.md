# zeroslop — ADAPTER: WITH-CURSOR
> Use zeroslop inside Cursor projects.
> zeroslop adds COLD-READ grounding + quality gates to your Cursor workflow.

---

## Setup

In Cursor, add zeroslop files to your project context:

```
1. Add BOOT.md content to your .cursorrules file
   OR paste it into the Cursor system prompt

2. Keep 01-COLD-READ.md open in a tab — reference it 
   when starting work on any existing file

3. After Cursor generates any feature, run the gate 
   manually by pasting the relevant gate file and 
   asking: "run this gate on what you just built"
```

---

## Workflow With Cursor

```
CURSOR HANDLES:       Code generation, autocomplete,
                      file navigation, refactoring

ZEROSLOP HANDLES:     Pre-build validation (SCOUT + VALIDATE)
                      Codebase grounding (COLD-READ)
                      Post-build gates (SECURITY, DESIGN, QA)
                      Self-scoring enforcement
```

---

## The Cursor + zeroslop Loop

```
1. Open project in Cursor
2. Paste BOOT.md into Cursor chat at session start
3. Cursor reads your existing files automatically
   (this IS COLD-READ — confirm conventions match)
4. Describe feature → Cursor builds
5. After build: paste SECURITY-GATE.md → run audit
6. After security: paste QA-AGENT.md → self-score
7. Score < 70 → ask Cursor to rebuild (not patch)
8. Score ≥ 70 → proceed to next feature
```

---

## .cursorrules Template

Add this to your `.cursorrules` file to embed zeroslop defaults:

```
# zeroslop rules — applied to all Cursor generations

## Code quality
- Never write stubs or TODO comments
- Never hardcode credentials — use config files
- All DB queries use prepared statements
- CSRF tokens on all state-changing forms
- Self-score every feature after building

## Conventions
- Use existing utility functions from this codebase
- Match existing naming conventions exactly
- Flag any deviation: DEVIATION: [what and why]
- Flag any assumption: ASSUMPTION: [X] — confirm or correct

## Design
- Never use Inter or Roboto as display font
- Never use purple gradient on white background
- Every input needs 3 states: default, focus, error
- Every card needs a hover state
- Test mobile at 375px before calling done

## Standards
- Score below 70/100 = rebuild, not patch
- "This should work" is not verification
- Describe the exact test path or admit it's incomplete
```

---

*zeroslop — Adapter: WITH-CURSOR*
