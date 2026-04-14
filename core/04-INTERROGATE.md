# zeroslop — 04-INTERROGATE
> Activates after VALIDATE returns BUILD or BUILD WITH CHANGES.
> This is the precision protocol. Every question changes a real file.

---

## What INTERROGATE Does

Most AI assistants ask questions to seem thorough.
zeroslop asks questions to unlock specific code decisions.

The difference:
```
GENERIC QUESTION:   "Who is your target audience?"
ZEROSLOP QUESTION:  "Do multiple users collaborate on the same idea,
                    or does each idea have exactly one owner?
                    This determines whether ideas table needs a 
                    collaborators pivot table or just an owner_id column."
```

Generic questions feel helpful. They waste time.
Zeroslop questions feel sharp. They prevent wrong architecture.

INTERROGATE produces a complete picture of every decision
that cannot be inferred from the idea alone.
After INTERROGATE, there are no open architecture questions.
RATE can score the requirement. ORCHESTRATE can assign the work.
The build can begin without mid-build course corrections.

---

## TRIGGER CONDITIONS

INTERROGATE activates:
```
✅ Automatically after VALIDATE returns BUILD verdict
✅ Automatically after VALIDATE returns BUILD WITH CHANGES (agreed)
```

INTERROGATE does NOT activate:
```
❌ Before VALIDATE completes
❌ On feature requests for existing products (use COLD-READ context instead)
❌ When all decisions can be inferred from existing CODEBASE-DNA
```

If GROUNDED MODE is active (COLD-READ already ran):
Cross-reference every question against CODEBASE-DNA first.
If the answer already exists in the codebase — do not ask.
Only ask what the codebase cannot answer.

---

## QUESTION RULES
### Non-negotiable. Every single question must pass all four rules.

**RULE 1 — EVERY QUESTION MUST UNLOCK SOMETHING SPECIFIC**
Before asking any question, state what it unlocks:
```
[Q1] UNLOCKS: DB schema — whether ideas table needs collaborators pivot
[Q2] UNLOCKS: Architecture — whether to use WebSockets or polling
[Q3] UNLOCKS: Scope — whether notifications are in MVP or Phase 2
```
If you cannot state what a question unlocks — do not ask it.

**RULE 2 — MAXIMUM 7 QUESTIONS PER SESSION**
Force yourself to prioritize.
If you have 12 questions, find the 7 that unlock the most.
Rank by impact on architecture. Ask only the top 7.

**RULE 3 — NEVER ASK WHAT YOU CAN INFER**
If the answer is reasonably derivable from:
- The idea description
- SCOUT data
- VALIDATE findings
- CODEBASE-DNA (if GROUNDED MODE is active)
...do not ask. State your inference explicitly instead:
`INFERENCE: [X] based on [evidence]. Correct me if wrong.`

**RULE 4 — QUESTIONS ARE BINARY OR MULTIPLE CHOICE**
Open-ended questions produce rambling answers that still leave
architecture decisions open.
Every question must have 2-4 specific options.
Each option must be labeled with what it changes:

```
[Q1] Do users collaborate on ideas together, or does each 
     idea have a single owner?

     A) Single owner only
        → ideas table: owner_id column only
        → simpler auth checks on all idea operations
        
     B) Multiple collaborators allowed
        → needs idea_collaborators pivot table
        → needs invitation/request system
        → adds ~4 files and 2 DB tables to scope
```

The user picks A or B. Architecture is decided. No ambiguity.

---

## QUESTION CATEGORIES

Questions only come from these categories.
Any question that does not fit a category should not be asked.

```
CATEGORY 1 — DATA OWNERSHIP
  Who owns what data? 
  Can multiple users share ownership of the same record?
  What happens to data when a user is deleted?
  
  Example: "When a team project is archived, does it belong
  to the creator, all collaborators, or the institution?"

CATEGORY 2 — REAL-TIME vs ASYNC
  Does this feature need to update without page refresh?
  Does this trigger immediate notifications to other users?
  
  Example: "When someone upvotes an idea, does the vote 
  count update instantly for all viewers, or on next load?"
  
  Impact: Real-time = WebSockets or SSE. Async = simple DB + polling.
  These are fundamentally different architectures.

CATEGORY 3 — SCOPE BOUNDARY
  Is this feature in MVP or a later phase?
  Is this a core feature or a nice-to-have?
  
  Example: "Is the Forge engine (workshops, bootcamps, Demo Day)
  in MVP or Phase 2? This adds ~6 DB tables and 12 handlers
  to the initial build scope."

CATEGORY 4 — PERMISSION LOGIC
  Who can do what?
  Are there actions that require approval before completing?
  Are there features with role-based access?
  
  Example: "Can any student post an idea, or does it require
  faculty approval before it appears in the feed?"
  
  Impact: Approval flow = status column + notification triggers + 
  admin review queue. No approval = direct insert to feed.

CATEGORY 5 — RELATIONSHIP CARDINALITY
  One-to-one? One-to-many? Many-to-many?
  This determines the entire DB schema design.
  
  Example: "Can a student be a Visionary on one idea and a 
  Builder on a different idea simultaneously?"
  
  Impact: YES = role is per-idea (idea_members pivot table)
          NO = role is per-user (single role column on users table)

CATEGORY 6 — FAILURE AND EDGE BEHAVIOR
  What happens when something goes wrong?
  What happens at the boundary cases?
  
  Example: "If a Builder leaves a project mid-build, does
  the idea return to the feed looking for a new Builder,
  or does it get paused, or does it proceed without them?"
  
  Impact: Each answer adds or removes entire features from scope.

CATEGORY 7 — EXTERNAL DEPENDENCIES
  Does this feature depend on a third-party service?
  What happens if that service is unavailable?
  
  Example: "Is GitHub integration required for MVP launch,
  or is it an enhancement? If GitHub API is down, 
  should the feature fail gracefully or block the feature?"
```

---

## THE INTERROGATION FORMAT

Present all questions at once. Do not drip them one at a time.
The user answers all at once. You process all answers at once.
This is efficient. One round of questions. One round of answers.

Format:
```
INTERROGATE — [N] questions before architecture is locked.
Every answer below changes specific files in the build.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Q1] UNLOCKS: [what this decides]
[Question in plain language]

  A) [Option A] → [what this means for the build — specific]
  B) [Option B] → [what this means for the build — specific]
  C) [Option C if needed] → [what this means]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Q2] UNLOCKS: [what this decides]
[Question in plain language]

  A) [Option A] → [build impact]
  B) [Option B] → [build impact]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Continue for all questions]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

INFERENCES (things I determined without asking):
  → [Inference 1] based on [evidence]
  → [Inference 2] based on [evidence]
  
  Correct any of these that are wrong before answering above.
```

---

## PROCESSING ANSWERS

After the user answers all questions, process each answer and
output an ARCHITECTURE DECISIONS LOG:

```
ARCHITECTURE DECISIONS LOG
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Q1] → User chose: [A/B/C]
  Decision locked: [what was decided]
  Impact: [specific files/tables/features this affects]

[Q2] → User chose: [A/B/C]
  Decision locked: [what was decided]
  Impact: [specific files/tables/features this affects]

[Continue for all answers]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SCOPE CHANGE SUMMARY:
  Features added by answers:    [list if any]
  Features removed by answers:  [list if any]
  Net scope change:             [LARGER / SMALLER / SAME]

All decisions are locked. Proceeding to RATE.
```

---

## WHAT TO DO WITH CONFLICTING ANSWERS

Sometimes a user's answers contradict each other.
Flag it immediately. Do not silently resolve it.

```
CONFLICT DETECTED:
  Q2 answer: "Real-time notifications required"
  Q4 answer: "Budget is zero, hosting is shared XAMPP"
  
  These conflict. Real-time notifications require WebSockets
  or a service like Pusher. Shared XAMPP hosting does not
  support persistent connections.
  
  Resolution options:
  A) Keep real-time → needs upgraded hosting (cost implication)
  B) Change to polling every 30 seconds → works on XAMPP
  C) Defer real-time to Phase 2 → MVP uses polling
  
  Which do you prefer?
```

Do not proceed until the conflict is resolved.
A conflict in requirements = a conflict in the codebase.
Catch it here. Not at 2am during the build.

---

## WHAT INTERROGATE DOES NOT DO

```
❌ Does not ask about business model or monetization
❌ Does not ask about marketing or launch strategy
❌ Does not ask about team size or hiring plans
❌ Does not ask what makes the idea unique (SCOUT + VALIDATE did that)
❌ Does not ask open-ended questions with no specific options
❌ Does not ask more than 7 questions
❌ Does not ask follow-up questions after answers are given
   (If an answer is unclear — ask for clarification on that one point only)
```

---

## INTERROGATE → RATE HANDOFF

After all questions are answered and the ARCHITECTURE DECISIONS LOG
is complete, automatically transition to STAGE 5 — RATE.

Tell the user:
```
INTERROGATE COMPLETE.

[N] architecture decisions locked.
Scope is now defined with precision.

Moving to RATE.
I will score the full requirement before the build begins.
```

---

*zeroslop — 04-INTERROGATE*
*Part of the zeroslop methodology: github.com/harshithgangaraju/zeroslop*
