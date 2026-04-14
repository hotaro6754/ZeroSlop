# zeroslop — PROFILE: Healthcare
> Accessibility and compliance-heavy weights.
> Load alongside BOOT.md when building health or medical tools.

---

## When to use this profile
```
✅ Patient management platforms
✅ Health tracking applications
✅ Medical workflow tools
✅ Wellness and mental health products
✅ Clinical decision support tools
```

---

## ADJUSTED SCORING WEIGHTS

```
Standard zeroslop:    Backend 25 / Frontend 20 / Data 15 /
                      Connect 15 / Quality 15 / Evidence 10

Healthcare profile:   Security        35 pts  (patient data is sacred)
                      Accessibility   25 pts  (WCAG AA minimum, AAA preferred)
                      Data            20 pts  (integrity + privacy)
                      Frontend        10 pts  (-10)
                      Quality         10 pts  (-5)
                      Evidence        0 pts   (absorbed into Security)
```

Rationale: Healthcare products handle the most sensitive
personal data that exists. A privacy failure is a human harm,
not a business problem. Accessibility is not optional —
patients of all abilities need to access their health information.

---

## HEALTHCARE-SPECIFIC GATE ADDITIONS

```
PATIENT DATA PRIVACY:
  PII (name, DOB, diagnosis, etc.) never in URL parameters
  PII never in browser localStorage
  PII never in server logs
  Session timeout for inactive sessions (max 30 min)
  Data access is logged (who accessed what, when)
  Verified: [Y/N]

ACCESSIBILITY (WCAG AA minimum):
  All images have descriptive alt text
  All form inputs have associated labels (not just placeholder)
  Color is never the only way to convey information
  Contrast ratio minimum 4.5:1 for normal text
  Contrast ratio minimum 3:1 for large text
  All interactive elements reachable by keyboard
  Focus indicator visible on all interactive elements
  Error messages associated with their fields via aria
  Verified: [Y/N]

DATA ACCURACY:
  Medical values (dosages, measurements) validated for range
  Units always displayed with values (mg, ml, bpm, etc.)
  No rounding that could affect clinical interpretation
  Verified: [Y/N]
```

---

## HEALTHCARE DESIGN STANDARDS

```
Reference category:  HEALTHCARE
Style modifiers:     minimal.gallery (calm, clinical clarity)
                     (avoid dark.design — dark themes reduce
                      readability for older or impaired users)

Color rules specific to healthcare:
  ✅ High contrast — never sacrifice readability for aesthetics
  ✅ Status colors must have non-color indicator too
     (icon + color, not color alone)
  ✅ Error states must be immediately visible
  ❌ Red for anything except critical alerts (red = danger in medical)
  ❌ Dark backgrounds as primary surface (accessibility concerns)
  ❌ Small text for clinical data (minimum 16px for medical values)

Signature elements for healthcare:
  → Status indicators with icon + color + text label
  → Progress indicators for multi-step clinical flows
  → Confirmation dialogs for all irreversible actions
  → Clear timestamps on all health data entries
  → Print-friendly view for records

Anti-patterns for healthcare:
  ❌ Gamification elements (trivializes health context)
  ❌ Auto-save without confirmation for critical data
  ❌ Pagination that hides critical patient history
  ❌ Modals that block access to referenced data
  ❌ Any feature that could distract from critical information
```

---

## HEALTHCARE SELF-SCORE THRESHOLD

Standard rebuild threshold: 70/100
Healthcare rebuild threshold: **80/100**

Automatic rebuild regardless of score:
- Any WCAG AA accessibility failure
- Any patient PII in URL or localStorage
- Any color-only status indicator (no icon or text)
- Session that doesn't timeout

---

*zeroslop — Profile: Healthcare*
