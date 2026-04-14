# zeroslop — DESIGN-GATE
> Runs after UI-AGENT completes each frontend layer.
> Uses DESIGN-INTEL report as the standard. No defaults accepted.

---

## What DESIGN-GATE Does

UI-AGENT built something.
DESIGN-GATE checks it against the DESIGN-INTEL brief.

Not against generic standards.
Against the specific system locked for THIS project.

If UI-AGENT ignored the brief and built generic → REJECTED.
If UI-AGENT followed the brief but missed slop → REJECTED.
If UI-AGENT built exactly to spec with no slop → PASSED.

---

## THE GATE CHECKS

### CHECK 1 — COLOR SYSTEM COMPLIANCE
```
Are the CSS variables from DESIGN-INTEL actually used?
Or did UI-AGENT hardcode values anyway?

✅ PASS: All colors reference --css-variable system
❌ FAIL: Any hardcoded hex outside the variable definitions

Spot check:
  Open any component file.
  Search for: #[hex] or rgb( or hsl(
  If found outside variable definitions → FAIL
```

### CHECK 2 — TYPOGRAPHY COMPLIANCE
```
Are the specified fonts actually loaded and applied?
Is the type scale from DESIGN-INTEL used?

✅ PASS: Specified fonts loaded, scale applied consistently
❌ FAIL: Inter/Roboto/Arial still present
❌ FAIL: Font sizes deviate from locked scale
❌ FAIL: Font not loaded (just specified in CSS but 404s)
```

### CHECK 3 — COMPONENT SPEC COMPLIANCE
```
Do built components match the spec in DESIGN-INTEL?

For each component type:
  Button: [matches spec Y/N]
  Card:   [matches spec Y/N]
  Input:  [matches spec Y/N]
  Nav:    [matches spec Y/N]
  Badge:  [matches spec Y/N]

✅ PASS: All components match spec
❌ FAIL: Any component reverted to generic Bootstrap/default style
```

### CHECK 4 — MOTION SYSTEM COMPLIANCE
```
Is the motion profile from DESIGN-INTEL implemented?

✅ PASS: Entry animations, hover states, transitions all present
❌ FAIL: No animations at all
❌ FAIL: Animations deviate from locked duration/easing values
❌ FAIL: Hover states missing on interactive elements
```

### CHECK 5 — SLOP DETECTION (final pass)
```
Run the full slop checklist from 02b-DESIGN-SCOUT:

❌ Purple/indigo gradient on white background
❌ Inter or Roboto as primary display font
❌ Generic blue CTA with no brand identity
❌ Lorem ipsum or placeholder text
❌ Empty states that render nothing
❌ Loading = just a spinner
❌ Mobile = desktop shrunk (test at 375px)
❌ Buttons with no hover state
❌ Forms with no error/success state
❌ Cards with no hover interaction
❌ Symmetric identical-size card grid
❌ Nav with no scroll behavior

Slop flags found: [N]
0 = PASS
1-2 = FIX before moving on
3+ = REJECT — rebuild the layer
```

### CHECK 6 — MOBILE AT 375PX
```
Test every page/component at 375px viewport width.

✅ PASS: Content contained, readable, navigable
❌ FAIL: Any overflow, any invisible nav, any text below 12px,
         any button below 44px touch target, any broken grid
```

### CHECK 7 — SIGNATURE ELEMENT PRESENT
```
The DESIGN-INTEL report specified ONE signature UI element.
That thing that makes this product recognizable.

Is it present and implemented correctly?

✅ PASS: Signature element exists and works
❌ FAIL: Generic replacement used instead
❌ FAIL: Signature element present but broken/incomplete
```

---

## GATE RESULT

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
DESIGN-GATE RESULT: [Feature/Layer Name]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Color compliance:     ✅ / ❌
Typography:           ✅ / ❌
Component spec:       ✅ / ❌
Motion system:        ✅ / ❌
Slop detection:       ✅ / ❌  ([N] flags)
Mobile at 375px:      ✅ / ❌
Signature element:    ✅ / ❌

GATE: PASSED ✅ / BLOCKED ❌

[If BLOCKED]:
  Issues to fix: [specific list]
  Do not proceed to SECURITY-GATE until resolved.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

*zeroslop — DESIGN-GATE*
