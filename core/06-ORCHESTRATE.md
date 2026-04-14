# zeroslop — 06-ORCHESTRATE
> Activates after RATE returns 70+ with no blockers.
> This is the build machinery protocol. Work gets broken into agents. Agents have dependencies. Nothing ships without passing its gate.

---

## What ORCHESTRATE Does

Most AI builds are linear and fragile.
One big prompt. One big response. One big mess to debug.

zeroslop builds are structured and traceable.
Work is broken into agents. Each agent owns exactly one concern.
Each agent has a dependency — what must be done before it starts.
Each agent has a gate — what must be true before it hands off.

When something breaks, you know exactly which agent broke it.
When something is incomplete, you know exactly which gate failed.
There is no "it should work" in a zeroslop build.
There is only "gate passed" or "gate failed."

---

## TRIGGER CONDITIONS

ORCHESTRATE activates:
```
✅ Automatically after RATE returns PROCEED or PROCEED WITH CAUTION
✅ When user explicitly says "start the build" after RATE completes
```

ORCHESTRATE requires:
```
- RATE block completed (scope is known)
- Architecture decisions locked (INTERROGATE complete)
- Phase 1 scope defined (what is in MVP)
```

---

## THE STANDARD AGENT STACK

These are the seven standard agents in zeroslop.
Every build uses a subset of these. The order never changes.

```
AGENT 1 — DB-AGENT
  Owns:     Database schema design and all migrations
  Input:    Architecture decisions from INTERROGATE
  Output:   Complete schema — every table, column, index, FK
  Gate:     Schema is normalized, no missing FKs, 
            indexes on all queried columns
  Blocks:   Everything. Nothing else starts until DB-AGENT gates.

AGENT 2 — AUTH-AGENT
  Owns:     Authentication, session management, role system
  Input:    DB-AGENT output + auth pattern from COLD-READ
  Output:   Working login, logout, session, role checks
  Gate:     Every role can log in, every protected route 
            rejects unauthenticated users
  Depends:  DB-AGENT must gate first

AGENT 3 — BACKEND-AGENT
  Owns:     All business logic handlers and API endpoints
  Input:    DB-AGENT schema + AUTH-AGENT session system
  Output:   Every handler for every Phase 1 feature
  Gate:     Every handler processes correctly, returns expected
            response, handles error cases explicitly
  Depends:  DB-AGENT + AUTH-AGENT must gate first

AGENT 4 — UI-AGENT
  Owns:     All frontend pages, components, and interactions
  Input:    BACKEND-AGENT handlers + project conventions
  Output:   Every page connected to real backend endpoints
  Gate:     No dead buttons, no placeholder text, 
            works at 375px, slop detection passes
  Depends:  BACKEND-AGENT must gate first

AGENT 5 — SECURITY-AGENT
  Owns:     Security audit across all layers
  Input:    Everything built by agents 1-4
  Output:   Security issues fixed, not just listed
  Gate:     CSRF on all forms, PDO on all queries,
            no credentials in code, inputs validated
  Depends:  UI-AGENT must gate first

AGENT 6 — QA-AGENT
  Owns:     Self-scoring and verification of all features
  Input:    Everything built by agents 1-5
  Output:   Self-score block for every feature, 
            rebuild orders for anything below 70
  Gate:     Every feature scores 70+, 
            every feature has a verification path described
  Depends:  SECURITY-AGENT must gate first

AGENT 7 — FINE-TUNE-AGENT
  Owns:     Consistency pass against CODEBASE-DNA
  Input:    All completed features + CODEBASE-DNA
  Output:   Code that fits the existing codebase perfectly
  Gate:     No duplicate utilities, conventions match,
            all integrations connect correctly
  Depends:  QA-AGENT must gate first
  Note:     Only runs if GROUNDED MODE is active
```

---

## THE DEPENDENCY GRAPH

This is the visual representation of agent flow.
Present this to the user at the start of every build.

```
┌─────────────────────────────────────────────────────┐
│  ZEROSLOP BUILD GRAPH                               │
├─────────────────────────────────────────────────────┤
│                                                     │
│  [DB-AGENT]                                         │
│      │                                              │
│      │ gate: schema complete                        │
│      ▼                                              │
│  [AUTH-AGENT]                                       │
│      │                                              │
│      │ gate: all roles authenticated                │
│      ▼                                              │
│  [BACKEND-AGENT]                                    │
│      │                                              │
│      │ gate: all handlers verified                  │
│      ▼                                              │
│  [UI-AGENT]                                         │
│      │                                              │
│      │ gate: slop check passed, 375px verified      │
│      ▼                                              │
│  [SECURITY-AGENT]                                   │
│      │                                              │
│      │ gate: CSRF, PDO, no hardcoded credentials    │
│      ▼                                              │
│  [QA-AGENT]                                         │
│      │                                              │
│      │ gate: all features score 70+                 │
│      ▼                                              │
│  [FINE-TUNE-AGENT] ← only if GROUNDED MODE active  │
│      │                                              │
│      │ gate: conventions match, no duplicates       │
│      ▼                                              │
│  FEATURE COMPLETE                                   │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## TASK DECOMPOSITION

Before assigning agents, break Phase 1 scope into atomic tasks.
Each task must be:

```
- Small enough to complete and verify independently
- Assigned to exactly one agent
- Described with a specific verification step
- Tagged with the files it touches
```

Use this format for every task:

```xml
<task>
  <id>T001</id>
  <agent>DB-AGENT</agent>
  <name>Create users table</name>
  <files>migrations/001_create_users.sql</files>
  <action>
    Define users table with: id, roll_no (unique), full_name, 
    email, branch, batch, role, points, created_at
  </action>
  <verify>
    Run migration → table exists → INSERT test row → 
    SELECT returns row → roll_no uniqueness constraint blocks duplicate
  </verify>
  <done>users table exists with all columns and constraints</done>
  <depends_on>none</depends_on>
</task>

<task>
  <id>T002</id>
  <agent>DB-AGENT</agent>
  <name>Create ideas table</name>
  <files>migrations/002_create_ideas.sql</files>
  <action>
    Define ideas table with: id, owner_id (FK→users.id), 
    title, description, category, status, upvotes, created_at
  </action>
  <verify>
    Run migration → table exists → FK constraint to users → 
    INSERT idea with valid owner_id succeeds → 
    INSERT idea with invalid owner_id fails (FK violation)
  </verify>
  <done>ideas table with FK constraint to users working</done>
  <depends_on>T001</depends_on>
</task>
```

Generate ALL tasks before any agent starts working.
The full task list is the build plan. Nothing gets built that isn't on the list.
Nothing on the list gets skipped.

---

## THE ORCHESTRATION OUTPUT

After RATE completes and before any code is written,
produce this full orchestration block:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ZEROSLOP BUILD ORCHESTRATION
Project: [name] — Phase 1
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AGENT ROSTER:
  DB-AGENT        [N] tasks
  AUTH-AGENT      [N] tasks
  BACKEND-AGENT   [N] tasks
  UI-AGENT        [N] tasks
  SECURITY-AGENT  [N] tasks (runs as audit pass)
  QA-AGENT        [N] tasks (runs as scoring pass)
  FINE-TUNE-AGENT [active / inactive — depends on GROUNDED MODE]

TOTAL TASKS:      [N]
ESTIMATED EFFORT: [N] hours / [N] days

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

FULL TASK LIST:
[All tasks in XML format — every task before any code]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

GATE CHECKLIST:
  □ DB-AGENT gate passed
  □ AUTH-AGENT gate passed
  □ BACKEND-AGENT gate passed
  □ UI-AGENT gate passed
  □ SECURITY-AGENT gate passed
  □ QA-AGENT gate passed (all features 70+)
  □ FINE-TUNE-AGENT gate passed [or N/A]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Ready to begin.
Type "start DB-AGENT" to begin schema design.
Type "skip to [agent name]" if a previous agent is already complete.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## AGENT HANDOFF PROTOCOL

When each agent completes its tasks, it must formally gate.
The gate is not optional. The gate is not implied.
The agent states explicitly that it is gating.

Gate format:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
[AGENT NAME] — GATE CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Tasks completed: [N/N]

Gate conditions:
  ✅ [condition 1 — specific and verifiable]
  ✅ [condition 2]
  ✅ [condition 3]
  ❌ [failed condition — if any]

Gate result: PASSED / FAILED

[If PASSED]:
  Handing off to [NEXT AGENT].
  [Next agent] can now begin.

[If FAILED]:
  Gate blocked on: [specific condition that failed]
  Action required: [exactly what needs to be fixed]
  Will not hand off until fixed.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

A failed gate does not pause the session.
It defines exactly what needs to be fixed.
Fix it. Re-gate. Then proceed.

---

## RUNNING AGENTS IN THIS SESSION

In a single AI session, you play all agents sequentially.
You are not literally multiple AI instances.
You switch roles by acknowledging the role switch explicitly.

Format for role switch:
```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SWITCHING TO: BACKEND-AGENT
DB-AGENT gate: ✅ PASSED
AUTH-AGENT gate: ✅ PASSED
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

I am now operating as BACKEND-AGENT.
My scope: business logic handlers only.
I do not touch schema. I do not touch frontend.
I use only the tables and utilities already defined.

Beginning task [T005]: [task name]
```

The role switch announcement does three things:
1. Confirms previous gates passed
2. States the new scope boundary
3. Prevents scope creep between agents

---

## SCOPE CREEP PREVENTION

During execution, you will notice things that could be improved
in a different agent's layer. You do not fix them inline.
You log them and continue.

Format:
```
SCOPE NOTE: [observation about a different layer]
  Layer:   [which agent owns this]
  Action:  Logged for [agent name] to address
  Impact:  [none / minor / blocking]
  Continuing with current task.
```

If a scope note is BLOCKING — stop the current agent.
Resolve the blocking issue in its correct agent layer first.
Then resume.

---

## PARALLEL TASKS

Some tasks within the same agent can run in parallel
(meaning: they can be described and built in the same response).

Tasks can be parallel if:
```
✅ They touch completely different files
✅ Neither depends on the output of the other
✅ Combined they do not exceed a single coherent response
```

Tasks must be sequential if:
```
❌ Task B needs the output of Task A
❌ They touch the same file
❌ One validates the other
```

State when tasks are parallel:
```
Running T003 and T004 in parallel:
  T003 → creates notifications table (independent)
  T004 → creates points_log table (independent)
  Neither depends on the other. Safe to build together.
```

---

## WHAT ORCHESTRATE DOES NOT DO

```
❌ Does not write any code — that is EXECUTE (Stage 7)
❌ Does not skip the task list and go straight to building
❌ Does not allow an agent to start before its dependency gates
❌ Does not allow a feature to complete without a gate check
❌ Does not treat "it looks done" as a gate pass
   Gates are specific and checkable — not subjective
```

---

## ORCHESTRATE → EXECUTE HANDOFF

After the full task list is generated and presented:

Tell the user:
```
ORCHESTRATE COMPLETE.

[N] tasks defined across [N] agents.
Dependency graph is locked.
All gates defined.

To begin:
  "start DB-AGENT" → begins schema design
  
Each agent will gate before the next begins.
Nothing ships without a gate pass.
```

---

*zeroslop — 06-ORCHESTRATE*
*Part of the zeroslop methodology: github.com/harshithgangaraju/zeroslop*
