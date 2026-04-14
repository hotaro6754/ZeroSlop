# zeroslop — PROFILE: Campus Platform
> Adjusted scoring weights for student and campus platforms.
> Built for IdeaSync-type projects. Load alongside BOOT.md.

---

## When to use this profile
```
✅ Student innovation platforms
✅ Campus community tools
✅ College event/workshop management
✅ Academic project tracking
✅ Student gamification systems
```

---

## ADJUSTED SCORING WEIGHTS

```
Standard zeroslop:    Backend 25 / Frontend 20 / Data 15 /
                      Connect 15 / Quality 15 / Evidence 10

Campus profile:       Frontend    30 pts  (+10 — students judge by UI)
                      Backend     20 pts  (-5)
                      Data        20 pts  (+5 — gamification integrity critical)
                      Quality     15 pts  (unchanged)
                      Connect     10 pts  (-5)
                      Evidence    5 pts   (-5)
```

Rationale: Students adopt based on feel and speed.
If it looks bad on mobile or feels slow, adoption fails.
Gamification data integrity is critical — points manipulation
destroys trust in the entire platform overnight.

---

## CAMPUS-SPECIFIC GATE ADDITIONS

```
GAMIFICATION INTEGRITY:
  Points awarded ONLY via awardPoints() — never inline UPDATE
  Points log entry created for every award
  No way to award points twice for same action
  Leaderboard reflects real points_log data
  Integrity verified: [Y/N]

MOBILE-FIRST:
  Campus platforms are used on phones, always.
  375px is not a breakpoint to support.
  It is the primary viewport.
  All features must work perfectly at 375px.
  Desktop is the enhancement, not mobile.

ROLL NUMBER AUTH:
  Roll number format validated (institute-specific pattern)
  Roll number uniqueness enforced at DB level (UNIQUE constraint)
  Roll number used as primary identifier in all sessions
  Verified: [Y/N]

PERMANENT ARCHIVE:
  Completed projects are never deleted — only archived
  Archive is publicly browsable (confirm intent)
  Student data persists after graduation (no CASCADE DELETE on users)
  Archive integrity: [Y/N]
```

---

## CAMPUS DESIGN STANDARDS

```
Reference category:  CAMPUS_PLATFORM
Style modifiers:     dark.design (optional — depends on brand)
                     godly.website (if going bold/modern)

Signature elements for campus platforms:
  → Achievement badges / tier indicators
  → Public leaderboard with animation on rank change
  → Idea feed with real-time upvote count
  → Builder profile with GitHub contribution card
  → Demo Day countdown / upcoming event widget

Anti-patterns for campus platforms:
  ❌ Desktop-only layouts (students use phones)
  ❌ Overly corporate/formal visual language
  ❌ No gamification feedback (silent point awards)
  ❌ Anonymous idea posting (ownership matters for credit)
  ❌ Complex multi-step forms on mobile
```

---

## CAMPUS SELF-SCORE THRESHOLD

Standard rebuild threshold: 70/100
Campus profile threshold: **70/100** (standard)

Automatic rebuild triggers specific to campus:
- Mobile breaks at 375px: automatic rebuild (students are on mobile)
- Points awarded inline (not via awardPoints()): automatic rebuild
- No empty state on idea feed: automatic rebuild

---

*zeroslop — Profile: Campus Platform*
