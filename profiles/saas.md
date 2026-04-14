# zeroslop — PROFILE: SaaS
> Adjusted scoring weights for SaaS products.
> Load this alongside BOOT.md when building a SaaS platform.

---

## When to use this profile
```
✅ B2B or B2C software-as-a-service
✅ Subscription-based web applications
✅ Dashboard-heavy products
✅ Multi-tenant platforms
```

---

## ADJUSTED SCORING WEIGHTS

```
Standard zeroslop:    Backend 25 / Frontend 20 / Data 15 /
                      Connect 15 / Quality 15 / Evidence 10

SaaS profile:         Security    30 pts  (+5 from Backend)
                      Frontend    25 pts  (+5)
                      Quality     20 pts  (+5 from Data)
                      Backend     15 pts  (-10)
                      Connect     10 pts  (-5)
                      Evidence    0 pts   (absorbed into Security)
```

Rationale: SaaS products live or die on security and design.
A security failure destroys trust. Poor UI destroys retention.
Code quality directly affects maintenance cost at scale.

---

## SAAS-SPECIFIC GATE ADDITIONS

Beyond standard gates, SaaS features must also pass:

```
MULTI-TENANCY CHECK:
  Can user A ever see user B's data?
  Are all queries filtered by owner/organization ID?
  Tenant isolation verified: [Y/N]

SUBSCRIPTION/PLAN CHECK (if applicable):
  Are paid features gated server-side (not just UI)?
  Can a free user access paid endpoints by direct URL?
  Plan enforcement: [Y/N]

PERFORMANCE CHECK:
  Any query that runs on every page load — is it cached?
  Any N+1 query patterns introduced?
  Dashboard loads in under 2 seconds with realistic data?
```

---

## SAAS DESIGN STANDARDS

```
Reference category:  B2B_ENTERPRISE or AI_SAAS
Style modifiers:     dark.design (if dark UI)
                     minimal.gallery (if clean/professional)

Signature elements for SaaS:
  → Command palette (Cmd+K)
  → Persistent sidebar with section navigation
  → Activity feed / audit log
  → Usage/quota meters
  → Empty onboarding state that guides setup

Anti-patterns for SaaS:
  ❌ Landing page aesthetic inside the dashboard
  ❌ No loading states on data-heavy tables
  ❌ Settings buried 3+ levels deep
  ❌ No keyboard shortcuts
  ❌ Toast notifications for destructive actions (use modal confirm)
```

---

## SAAS SELF-SCORE THRESHOLD

Standard rebuild threshold: 70/100
SaaS rebuild threshold: **75/100**

Security failure: automatic rebuild regardless of total score.

---

*zeroslop — Profile: SaaS*
