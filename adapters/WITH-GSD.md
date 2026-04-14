# zeroslop — ADAPTER: WITH-GSD
> Use zeroslop on top of get-shit-done (GSD).
> zeroslop wraps GSD's planning phases with intelligence and quality gates.

---

## How They Work Together

```
GSD handles:         Context engineering, XML task planning,
                     wave execution, structured build phases

zeroslop adds:       Pre-GSD intelligence (SCOUT + VALIDATE)
                     Codebase grounding (COLD-READ before any wave)
                     Post-wave gates (after each GSD wave completes)
                     Design intelligence (DESIGN-SCOUT before UI wave)
                     Self-scoring enforcement
```

GSD builds the right things in the right order.
zeroslop ensures what gets built is actually right.

---

## Workflow: GSD + zeroslop

```
PHASE 0 — INTELLIGENCE (zeroslop, before GSD starts)
  Run 02-SCOUT.md on the product idea
  Run 02b-DESIGN-SCOUT.md on existing/planned UI
  Run 03-VALIDATE.md to confirm approach
  Run 04-INTERROGATE.md to lock decisions
  Run 05-RATE.md to scope the work

PHASE 1 — CONTEXT (GSD)
  GSD builds your PRD and context files as normal
  Add CODEBASE-DNA.md (from COLD-READ) to GSD context
  Add DESIGN-INTEL.md (from DESIGN-SCOUT) to GSD context

PHASE 2 — PLANNING (GSD)
  GSD builds task lists in XML as normal
  zeroslop adds gate checkpoints between waves:
  <task>
    <n>DB wave complete</n>
    <gate>Run COMPLETENESS-GATE before BACKEND wave</gate>
  </task>

PHASE 3+ — WAVES (GSD + zeroslop gates)
  GSD executes each wave as normal
  After EACH wave: run the appropriate zeroslop gate
    DB wave done       → COMPLETENESS-GATE (schema check)
    Backend wave done  → COMPLETENESS-GATE + SECURITY-GATE
    UI wave done       → DESIGN-GATE
    Full feature done  → QA-AGENT self-score
    All features done  → REGRESSION-GATE
```

---

## Gate Insert Template for GSD Tasks

Add this to any GSD task XML to insert a zeroslop gate:

```xml
<task>
  <n>[Task name]</n>
  <file>[file]</file>
  <action>[what to build]</action>
  <verify>[test path]</verify>
  <zeroslop-gate>COMPLETENESS + SECURITY</zeroslop-gate>
  <zeroslop-threshold>70</zeroslop-threshold>
  <done>Gate passed, score ≥ 70</done>
</task>
```

---

*zeroslop — Adapter: WITH-GSD*
