# zeroslop — PROFILE: Fintech
> Security-heavy weights for financial products.
> Load alongside BOOT.md when building fintech or finance tools.

---

## When to use this profile
```
✅ Banking or payments applications
✅ Investment / trading platforms
✅ Financial dashboards
✅ Expense or budget tracking
✅ Crypto or DeFi interfaces
```

---

## ADJUSTED SCORING WEIGHTS

```
Standard zeroslop:    Backend 25 / Frontend 20 / Data 15 /
                      Connect 15 / Quality 15 / Evidence 10

Fintech profile:      Security    40 pts  (dominant — non-negotiable)
                      Data        25 pts  (+10 — financial data integrity)
                      Frontend    15 pts  (-5)
                      Backend     10 pts  (-15)
                      Quality     10 pts  (-5)
                      Evidence    0 pts   (absorbed into Security + Data)
```

Rationale: A financial product with a security flaw
is not a product. It is a liability. Period.
Data integrity is equally critical — financial figures
must be accurate to the cent, consistently, always.

---

## FINTECH-SPECIFIC GATE ADDITIONS

```
FINANCIAL DATA INTEGRITY:
  All monetary values stored as integers (cents) not floats
  No floating point arithmetic on financial calculations
  Transactions are atomic (all-or-nothing DB transactions)
  Every financial operation is logged with timestamp + user
  Reversal/rollback capability exists for failed operations
  Verified: [Y/N]

AUDIT TRAIL:
  Every action that touches money has an audit log entry
  Audit log is append-only (no UPDATE or DELETE on audit table)
  Audit includes: user_id, action, amount, timestamp, IP
  Verified: [Y/N]

RATE LIMITING:
  API endpoints that trigger financial operations are rate-limited
  Failed auth attempts are rate-limited and logged
  Verified: [Y/N]

DATA ENCRYPTION:
  Sensitive data (account numbers, etc.) encrypted at rest
  HTTPS enforced — no mixed content
  No sensitive data in URL parameters
  Verified: [Y/N]
```

---

## FINTECH DESIGN STANDARDS

```
Reference category:  FINTECH
Style modifiers:     dark.design (precision dark surfaces)
                     minimal.gallery (data-forward minimalism)

Signature elements for fintech:
  → Real-time number updates with smooth count animation
  → Color-coded gain/loss (green/red with accessibility consideration)
  → Dense data tables with sort + filter + export
  → Chart tooltips with precise values on hover
  → Transaction history with infinite scroll or pagination

Anti-patterns for fintech:
  ❌ Playful/casual visual language (erodes trust)
  ❌ Ambiguous number formatting (always show currency + decimal)
  ❌ No loading state on financial data (users assume data is live)
  ❌ Destructive actions without confirmation modal
  ❌ Session that doesn't timeout (financial apps need auto-logout)
```

---

## FINTECH SELF-SCORE THRESHOLD

Standard rebuild threshold: 70/100
Fintech rebuild threshold: **80/100**

Any security issue: automatic rebuild, no exceptions.
Any financial data integrity issue: automatic rebuild.
Floating point used for money: automatic rebuild.

---

*zeroslop — Profile: Fintech*
