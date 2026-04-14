# zeroslop — 02-DESIGN-SCOUT
> Activates after 02-SCOUT completes, before UI-AGENT begins.
> Studies reference-class design. Diagnoses user's existing UI. 
> Produces a surgical enhancement brief. UI-AGENT builds from this — not from defaults.

---

## What DESIGN-SCOUT Does

Most AI builds UI from defaults.
Generic components. Generic spacing. Generic motion.
The result looks like every other AI-generated interface.

DESIGN-SCOUT does something different.

**Step 1:** Studies reference-class websites in the user's product category
to understand what peak design looks like for that space.

**Step 2:** Reviews the user's existing design/code with that education.
Finds every flaw. Names it specifically. No vague feedback.

**Step 3:** Produces a DESIGN-INTEL report — not a mood board,
not a list of suggestions. A surgical brief that tells UI-AGENT
exactly what to build, what to fix, and what standard to hit.

The references are the education.
The user's code is the patient.
DESIGN-SCOUT is the diagnosis.

---

## TRIGGER CONDITIONS

```
✅ Activates after 02-SCOUT when user has pasted a PRD/README
✅ Activates when user pastes existing frontend code (HTML/CSS/JS/PHP/React)
✅ Activates when user pastes screenshots or describes existing UI
✅ Activates when COLD-READ found frontend files in the codebase
```

If user has NO existing design yet:
→ Run STEP 1 (reference study) only
→ Skip STEP 2 (nothing to critique)
→ Produce a DESIGN-BRIEF instead of a critique
→ UI-AGENT builds from that brief fresh

If user HAS existing design:
→ Run all three steps
→ Full critique + enhancement brief

---

## STEP 1 — REFERENCE STUDY
### AI studies peak-class design for the user's product category.

First, identify the product category from PRD/README:

```
CATEGORY DETECTION:
Read the PRD. Assign ONE primary category:

  AI_SAAS         → AI tools, AI platforms, model APIs
  DEVTOOL         → Developer tools, CLIs, SDKs, frameworks
  B2B_ENTERPRISE  → Enterprise SaaS, B2B platforms, dashboards
  FINTECH         → Finance, trading, banking, payments
  HEALTHCARE      → Health platforms, medical tools, wellness
  PRODUCTIVITY    → Workspace tools, note-taking, task management
  MARKETING       → Landing pages, agency sites, conversion tools
  DESIGN_TOOL     → Design platforms, creative tools, brand tools
  CAMPUS_PLATFORM → Student platforms, education tools, campus apps
```

Then activate the reference set for that category:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
REFERENCE LIBRARY — STUDY THESE FOR THE DETECTED CATEGORY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

AI_SAAS / AI_TOOL:
  Primary:   modal.com, langbase.com, antimetal.com
  Secondary: monoai.framer.website, composio.dev, adaline.ai
  Study for: Dark surfaces, noise textures, glow accents,
             code-forward layouts, bento grids, terminal aesthetics

DEVTOOL / DEVELOPER_PLATFORM:
  Primary:   composio.dev, invertase.io, keel.so
  Secondary: cap.so, dualite.dev, langbase.com
  Study for: Monospace type, dense information layout,
             syntax highlighting patterns, CLI aesthetics,
             documentation-adjacent design

B2B_ENTERPRISE / SAAS_PLATFORM:
  Primary:   miro.com, frontify.com, ada.cx
  Secondary: effortel.com, thalamusgme.com, clearstreet.io
  Study for: Trust signals, structured navigation,
             data density, table patterns, dashboard layouts,
             professional color restraint

FINTECH / FINANCE:
  Primary:   fey.com, clearstreet.io, slash.com
  Secondary: antimetal.com, meter.com
  Study for: Data visualization patterns, chart aesthetics,
             number typography, dark precision surfaces,
             financial dashboard density

HEALTHCARE:
  Primary:   silnahealth.com, para.co, phia.app
  Secondary: unlearn.ai, meetjamie.ai
  Study for: Clinical calm, trust typography, soft surfaces,
             accessibility-first layouts, status/progress patterns,
             compliance-aware design

PRODUCTIVITY / WORKSPACE:
  Primary:   caret.so, cap.so, swan.so
  Secondary: making.today, way.co, chroniclehq.com
  Study for: Focus-first layouts, minimal chrome, keyboard-friendly UI,
             sidebar patterns, command palette aesthetics,
             content-first hierarchy

MARKETING / AGENCY / LANDING:
  Primary:   clario.framer.website, superior-template.framer.website
             landerx.framer.website
  Secondary: humanvoiceover.com, making.today
  Study for: Hero impact, scroll narrative, conversion patterns,
             bold typography at scale, social proof design,
             CTA hierarchy and urgency

DESIGN_TOOL / CREATIVE:
  Primary:   dualite.dev, brand.ai, micro.so
  Secondary: chroniclehq.com, mobbin.com
  Study for: Canvas interfaces, tool palette patterns,
             drag-and-drop affordances, creative color use,
             design system documentation style

CAMPUS_PLATFORM / EDUCATION:
  Primary:   making.today, cap.so, caret.so
  Secondary: swan.so, para.co
  Study for: Student-friendly layouts, gamification patterns,
             community feed design, profile/achievement UI,
             mobile-first student experience
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

After selecting category references, also activate the
STYLE MODIFIER LIBRARY. These are curated design vaults —
each contains hundreds of elite examples filtered by aesthetic.
They overlay on top of category references to sharpen style direction.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
STYLE MODIFIER LIBRARY — ALWAYS STUDY ALONGSIDE CATEGORY REFS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

dark.design
  What it is:   500+ curated dark UI examples. All high-end.
                Sleek, moody, interface-focused.
  When to use:  ALWAYS when product uses dark surfaces.
                The definitive reference for dark UI done right.
  Study for:    Surface hierarchy in dark palettes,
                how elite products handle dark cards/borders/glow,
                what separates premium dark UI from generic dark UI,
                typography contrast on dark backgrounds,
                color accent usage in dark contexts.
  Key lesson:   Dark UI fails when it's just "black background."
                It succeeds when surface levels are distinct —
                base / surface / elevated / overlay — each with
                subtle but intentional differentiation.

godly.website
  What it is:   Curated vault of future-forward, bold, modern
                websites. Best of the web, design-forward.
  When to use:  When product needs visual boldness, motion,
                or needs to stand out from conservative category.
  Study for:    Hero layouts that break conventions,
                experimental typography at scale,
                scroll-driven narrative design,
                WebGL and shader backgrounds in production,
                how bold aesthetics stay functional,
                asymmetric grid usage that actually works.
  Key lesson:   Bold design isn't loud design. The best examples
                on Godly are bold in ONE dimension — type scale,
                or layout, or color — not all three simultaneously.

shadergradient.co
  What it is:   Interactive shader and gradient generator.
                Futuristic visual playground, WebGL-native.
  When to use:  When hero background needs depth beyond flat color.
                AI tools, creative platforms, tech products.
  Study for:    How animated gradients create depth without distraction,
                shader aesthetics that feel premium not tacky,
                color mesh techniques for hero backgrounds,
                how to use motion in backgrounds without hijacking
                the user's attention from the content.
  Key lesson:   Background motion must be SLOW and SUBTLE.
                If the background competes with the headline,
                the background loses — and so does the product.
                shadergradient.co shows the line between
                atmospheric and distracting.

minimal.gallery
  What it is:   Ultra-clean, typography-driven, premium minimalist
                inspiration. Curated from the web's best minimal work.
  When to use:  When product should feel premium, editorial,
                or intentionally restrained. Healthcare, legal,
                high-end SaaS, professional services.
  Study for:    How whitespace creates luxury perception,
                type-as-design-element (headline IS the visual),
                color restraint that still feels intentional,
                grid systems that breathe,
                how minimal sites handle feature sections
                without looking empty,
                what makes "minimal" feel rich vs. lazy.
  Key lesson:   The difference between minimal and unfinished
                is precision. Every spacing value is deliberate.
                Every font weight choice has a reason.
                Minimal.gallery shows what intentional restraint
                looks like at the highest level.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
STYLE MODIFIER SELECTION GUIDE:
  Product uses dark surfaces      → ALWAYS study dark.design
  Product needs visual boldness   → study godly.website
  Product needs hero background   → study shadergradient.co
  Product feels premium/restrained→ study minimal.gallery
  Default: study ALL FOUR         → synthesize what applies
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

For each reference site AND style modifier, use web search or fetch to extract
these 10 design signals:

```
SIGNAL 1 — BACKGROUND SYSTEM
  What is the base surface color?
  Light / Dark / Dual-mode?
  Solid / Gradient / Noise / Glassmorphic / Mesh?
  What gives it depth beyond flat color?

SIGNAL 2 — COLOR PALETTE  
  Brand primary: [exact value or description]
  Accent/CTA:    [color + usage]
  Surface:       [card/panel color]
  Border:        [divider color and weight]
  Text hierarchy:[3-4 levels from heading to muted]
  What makes this palette work for the category?

SIGNAL 3 — TYPOGRAPHY
  Display font:  [name + weight + size at hero]
  Body font:     [name + size + line-height]
  Code font:     [if present]
  Letter spacing:[tight / normal / loose — at which sizes?]
  What makes this type choice feel right for the product?

SIGNAL 4 — LAYOUT PATTERN
  Hero structure: [centered / left-aligned / split / full-bleed]
  Feature section:[bento / card grid / alternating / scrolling]
  Navigation:    [sticky / floating / sidebar / minimal]
  Grid system:   [12-col / 8-col / asymmetric / free-flow]
  What is unconventional or memorable about the layout?

SIGNAL 5 — SIGNATURE UI ELEMENT
  The ONE thing that makes this site recognizable.
  Examples: floating nav with blur / animated gradient orbs /
  glassmorphic cards / scrolling logo marquee / live metrics /
  interactive code blocks / split cursor / parallax layers
  Name it specifically. This is what elevates it beyond generic.

SIGNAL 6 — MOTION PROFILE
  Page load: [what animates on arrival]
  Scroll:    [what triggers on scroll — fade / slide / scale]
  Hover:     [card lift / glow / color shift / underline grow]
  CTA:       [shimmer / pulse / arrow move]
  Transitions:[page / section / modal transitions]
  Overall feel: Aggressive / Purposeful / Subtle / Invisible

SIGNAL 7 — COMPONENT FINGERPRINT
  Buttons:  [shape / weight / icon usage / hover behavior]
  Cards:    [border / shadow / background / hover state]
  Inputs:   [style / focus state / error state]
  Badges:   [style for status / tags / labels]
  Tables:   [if data-heavy — row style / hover / sorting UI]
  What makes these components feel designed, not default?

SIGNAL 8 — SPACING DENSITY
  Overall feel: Generous / Balanced / Dense
  Section padding: [top/bottom rhythm]
  Card internal: [content breathing room]
  Line height: [text density within blocks]
  What spacing decisions make this product feel premium?

SIGNAL 9 — WHAT THIS SITE DOES BRILLIANTLY
  Name the 2-3 specific design decisions that elevate this
  above generic AI-built sites. Be specific:
  Not "clean design" — "the hero uses a 3px border on cards
  with a 0.5px glow that creates depth without shadows"

SIGNAL 10 — WHAT THIS SITE GETS WRONG / WHAT IT'S MISSING
  This is critical. No site is perfect. Find the gaps:
  → Where does it fall into generic patterns?
  → What animation is overdone or distracting?
  → What component looks unfinished?
  → Where does it break on mobile?
  → What does the user probably complain about?
  These gaps become your user's opportunities.
```

After studying 3 primary references, synthesize into a
CATEGORY DESIGN STANDARD — what excellent looks like for this product type.

---

## STEP 2 — USER DESIGN CRITIQUE
### Review the user's existing design/code against that standard.

This step only runs if the user has existing frontend code or design.

Read every frontend file found in COLD-READ.
Look at: HTML structure, CSS classes, component files,
inline styles, Tailwind classes, color values, font imports.

Run a full audit across 12 dimensions:

---

### AUDIT DIMENSION 1 — BACKGROUND AND SURFACE SYSTEM

```
FOUND IN CODE:
  Background color(s): [what's actually there]
  Surface colors: [card/panel colors used]
  Depth method: [shadows? borders? none?]

DIAGNOSIS:
  ✅ GOOD:   [what works]
  ❌ FLAW:   [what's wrong — be specific]
  ⚠ GENERIC: [what's default/boring but not broken]

REFERENCE STANDARD:
  [Category] products use [what reference sites do]
  The gap: [specific difference between user's code and standard]

ENHANCEMENT:
  Replace [current] with [specific fix]
  Add [specific technique] to create [specific effect]
```

---

### AUDIT DIMENSION 2 — COLOR SYSTEM

```
FOUND IN CODE:
  Primary colors used: [list hex values or Tailwind classes]
  Accent colors: [what's used for CTAs and highlights]
  Text colors: [how many levels, what values]
  Consistency: [are color variables used or hardcoded everywhere?]

DIAGNOSIS:
  FLAWS FOUND:
  ❌ [specific flaw — e.g., "blue-500 used for CTAs but 
      blue-600 used for links — inconsistent signal"]
  ❌ [specific flaw — e.g., "gray-100 background creates 
      no visual hierarchy between surface levels"]
  ❌ [specific flaw — e.g., "no dark mode variables defined
      — hardcoded values will break if dark mode added"]
  ❌ [specific flaw — e.g., "accent color has 4.1:1 contrast
      ratio on white — fails WCAG AA on smaller text"]

GENERIC AI PATTERNS DETECTED:
  ❌ [e.g., "purple gradient on white — most common AI slop"]
  ❌ [e.g., "blue CTA on white — indistinguishable from default"]

ENHANCEMENT:
  Define CSS variables:
    --bg-base:     [value]
    --bg-surface:  [value]  
    --bg-elevated: [value]
    --accent:      [value]
    --text-1:      [value]
    --text-2:      [value]
    --text-3:      [value]
  Replace all hardcoded values with these.
  Reason: [why this system is better]
```

---

### AUDIT DIMENSION 3 — TYPOGRAPHY

```
FOUND IN CODE:
  Fonts loaded: [what font imports exist]
  Display font: [what's used for headings]
  Body font: [what's used for body text]
  Font sizes: [what scale is used — px or rem values]
  Line heights: [what values]
  Letter spacing: [any tracking applied?]
  Font weights: [which weights loaded and used]

DIAGNOSIS:
  ❌ [e.g., "Inter used everywhere — zero personality, 
      indistinguishable from 10,000 other AI-built sites"]
  ❌ [e.g., "h1 is 32px — too small for a hero headline, 
      reference class sites use 64-96px at this breakpoint"]
  ❌ [e.g., "no letter-spacing on uppercase labels — 
      they look like normal text instead of labels"]
  ❌ [e.g., "line-height 1.5 on all text — too loose for 
      headings, too tight for long-form paragraphs"]
  ❌ [e.g., "body and heading use same weight 400 — 
      no visual hierarchy between text levels"]

GENERIC AI PATTERNS DETECTED:
  ❌ Inter/Roboto/Arial as primary font
  ❌ Flat type scale with no display personality
  ❌ Missing font pairing (display + body)

ENHANCEMENT:
  Replace [current font] with [specific alternative] for display
  Reason: [why this font fits the product category]
  New scale:
    --text-hero:  [size / weight / tracking / line-height]
    --text-h1:    [size / weight / tracking / line-height]
    --text-h2:    [size / weight / tracking / line-height]
    --text-body:  [size / weight / tracking / line-height]
    --text-small: [size / weight / tracking / line-height]
    --text-label: [size / weight / tracking / line-height]
```

---

### AUDIT DIMENSION 4 — LAYOUT AND SPATIAL COMPOSITION

```
FOUND IN CODE:
  Layout method: [flexbox / grid / float / Bootstrap columns]
  Max content width: [what container width is used]
  Section padding: [what vertical spacing between sections]
  Component spacing: [what gap between cards/items]
  Grid structure: [how many columns, what breakpoints]

DIAGNOSIS:
  ❌ [e.g., "max-w-4xl container is too narrow — 
      reference sites use max-w-7xl with wider breathing room"]
  ❌ [e.g., "all sections have identical py-8 padding — 
      no rhythm variation makes the page feel monotonous"]
  ❌ [e.g., "3-column grid collapses to 1 on mobile with 
      no intermediate 2-column state — jarring on tablet"]
  ❌ [e.g., "feature grid is symmetrical — every card 
      identical size — no visual weight variation"]
  ❌ [e.g., "hero section is left-padded same as body sections — 
      no full-bleed moment to create hierarchy"]

SLOP LAYOUTS DETECTED:
  ❌ All sections centered, same width, same padding
  ❌ Cards all same size in perfectly even grid
  ❌ No asymmetry, no visual tension, no memorable moment

ENHANCEMENT:
  [Specific layout changes with exact measurements]
  [Grid restructure with specific column patterns]
  [Spacing rhythm system to replace uniform padding]
```

---

### AUDIT DIMENSION 5 — COMPONENT QUALITY

Check every component type found in the code:

```
BUTTONS:
  Found: [what button styles exist]
  Flaws:
    ❌ [e.g., "rounded-md on all buttons — generic default"]
    ❌ [e.g., "no hover state beyond color change — no motion"]
    ❌ [e.g., "loading state not designed — button just freezes"]
    ❌ [e.g., "icon buttons have no tooltip — accessibility gap"]
  Enhancement: [specific button system to replace current]

CARDS:
  Found: [what card styles exist]
  Flaws:
    ❌ [e.g., "white bg with gray-200 border — looks like 
        Bootstrap default from 2018"]
    ❌ [e.g., "no hover state — cards feel static and dead"]
    ❌ [e.g., "drop-shadow-sm creates muddy blur, not crisp depth"]
    ❌ [e.g., "card padding inconsistent — some 16px some 24px"]
  Enhancement: [specific card system]

FORMS AND INPUTS:
  Found: [what input styles exist]
  Flaws:
    ❌ [e.g., "no focus ring — impossible to tell which 
        field is active — accessibility failure"]
    ❌ [e.g., "error state is just red border — 
        no error message position designed"]
    ❌ [e.g., "placeholder text color same as input text — 
        unreadable when field is empty"]
    ❌ [e.g., "submit button adjacent to inputs but 
        not visually grouped — form looks disconnected"]
  Enhancement: [specific form system with 3 states each]

NAVIGATION:
  Found: [what nav structure exists]
  Flaws:
    ❌ [e.g., "nav has no scroll behavior — stays white 
        and loses visual separation from content below"]
    ❌ [e.g., "mobile nav is just hidden links, 
        no hamburger animation, no slide-in panel"]
    ❌ [e.g., "active page indicator missing — 
        user can't tell where they are"]
  Enhancement: [specific nav improvements]

EMPTY STATES:
  Found: [are empty states designed or just "no data"]
  Flaws:
    ❌ [e.g., "empty tables just show nothing — 
        user thinks it's broken, not empty"]
    ❌ [e.g., "no illustration or icon in empty state — 
        just gray text on white background"]
  Enhancement: [specific empty state design for each component]

LOADING STATES:
  Found: [what loading patterns exist]
  Flaws:
    ❌ [e.g., "loading spinner for everything — 
        no skeleton screens — content feels like it disappears"]
    ❌ [e.g., "no loading state on submit buttons — 
        user double-clicks thinking it didn't work"]
  Enhancement: [skeleton screens + button loading states]
```

---

### AUDIT DIMENSION 6 — MOTION AND ANIMATION

```
FOUND IN CODE:
  Transitions defined: [list transition/animation CSS found]
  Animations: [any keyframe animations found]
  Hover behavior: [what happens on hover]
  Page load: [any entry animations]

DIAGNOSIS:
  ❌ [e.g., "transition-colors on buttons — too short 
      and barely perceptible — feels laggy, not smooth"]
  ❌ [e.g., "no scroll animations — page feels static, 
      every section appears instantly like a document"]
  ❌ [e.g., "hover scales everything by 1.05 — 
      overused pattern that looks like a template"]
  ❌ [e.g., "form submission has no feedback animation — 
      user stares at frozen UI wondering if it worked"]
  ❌ [e.g., "modal appears instantly with no transition — 
      jarring visual cut in otherwise soft interface"]

MISSING ENTIRELY:
  ❌ No staggered list item reveals
  ❌ No micro-interaction on form success
  ❌ No hover depth on interactive cards
  ❌ No page transition between routes

ENHANCEMENT:
  Entry animations: [specific fade-up / stagger pattern]
  Hover system:     [specific hover behavior per component]
  Feedback motion:  [success / error / loading states]
  Duration scale:   [fast 150ms / normal 250ms / slow 400ms]
  Easing system:    [what easing curves to use and when]
```

---

### AUDIT DIMENSION 7 — MOBILE AND RESPONSIVE DESIGN

```
FOUND IN CODE:
  Breakpoints used: [what sm/md/lg/xl classes exist]
  Mobile nav: [how navigation adapts]
  Grid behavior: [how columns collapse]
  Typography scaling: [do font sizes scale down?]
  Touch targets: [are buttons large enough at 375px?]

DIAGNOSIS:
  ❌ [e.g., "hero headline is 48px on mobile — 
      overflows container on 375px viewport"]
  ❌ [e.g., "grid goes from 3-col directly to 1-col — 
      tablet users see 1 card per row in a wide space"]
  ❌ [e.g., "desktop nav is just hidden on mobile — 
      no mobile menu exists in the code"]
  ❌ [e.g., "card padding is 32px on all screens — 
      too cramped on 375px with this content density"]
  ❌ [e.g., "click targets are 28px — below the 44px 
      minimum for touch — fails mobile usability"]

CRITICAL FAILURES (automatic rebuild triggers):
  ⛔ Navigation inaccessible on mobile
  ⛔ Content overflow at 375px
  ⛔ Form inputs too small to tap accurately
  ⛔ Text below 12px at any breakpoint

ENHANCEMENT:
  [Specific responsive fixes with exact breakpoint values]
```

---

### AUDIT DIMENSION 8 — ACCESSIBILITY

```
FOUND IN CODE:
  ARIA labels: [what aria attributes exist]
  Alt text: [are images described]
  Focus management: [are focus styles visible]
  Color contrast: [any obvious contrast issues]
  Semantic HTML: [are headings, landmarks correct]

DIAGNOSIS:
  ❌ [specific accessibility failures found]
  
ENHANCEMENT:
  [Specific fixes — not a lecture, actionable changes]
```

---

### AUDIT DIMENSION 9 — DARK MODE READINESS

```
FOUND IN CODE:
  Dark mode support: [exists / partial / none]
  Color variables: [CSS vars used or hardcoded]
  Image handling: [are images dark-mode aware]

DIAGNOSIS:
  ❌ [e.g., "all colors hardcoded — dark mode would 
      require rewriting every component"]
  ❌ [e.g., "dark: classes exist on some components 
      but not others — inconsistent partial implementation"]

ENHANCEMENT:
  [Specific CSS variable system for dark mode]
  [Components to add dark: variants to]
```

---

### AUDIT DIMENSION 10 — VISUAL HIERARCHY AND FOCUS

```
FOUND IN CODE:
  What draws the eye first on page load?
  Is the primary CTA the most visually dominant element?
  Are secondary actions clearly subordinate?
  Is there visual clutter competing with key content?

DIAGNOSIS:
  ❌ [e.g., "three equally prominent CTAs on hero — 
      user doesn't know what to do first"]
  ❌ [e.g., "nav links same visual weight as hero headline — 
      no clear hierarchy"]
  ❌ [e.g., "card content has 4 equally sized elements — 
      no clear primary data point"]

ENHANCEMENT:
  [Specific hierarchy restructure]
```

---

### AUDIT DIMENSION 11 — GENERIC AI SLOP DETECTION

This runs on all code regardless of other findings.
These are instant rebuild triggers.

```
SLOP DETECTION SCAN:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

❌ Purple/indigo gradient on white background
   Found: [Y/N — location if found]
   Action: REBUILD — replace with category-appropriate palette

❌ Inter or Roboto as primary display font
   Found: [Y/N — location if found]
   Action: REPLACE — install distinctive font pair

❌ Generic blue (#3B82F6 / blue-500) as primary CTA
   Found: [Y/N — location if found]
   Action: REDESIGN — use brand-specific accent

❌ Lorem ipsum or placeholder text in UI
   Found: [Y/N — location if found]
   Action: REMOVE — replace with real or realistic content

❌ Empty state that renders nothing or says "No data"
   Found: [Y/N — location if found]
   Action: DESIGN — create intentional empty state

❌ Loading state that is just a spinner
   Found: [Y/N — location if found]
   Action: REPLACE — use skeleton screens

❌ Mobile layout that is desktop CSS with hidden overflow
   Found: [Y/N — location if found]
   Action: REBUILD — genuine mobile-first layout

❌ Buttons with no hover state beyond cursor pointer
   Found: [Y/N — location if found]
   Action: ADD — minimum: color shift + transition

❌ Forms with no designed error or success state
   Found: [Y/N — location if found]
   Action: DESIGN — 3 states minimum per input

❌ Cards with no hover interaction
   Found: [Y/N — location if found]
   Action: ADD — lift / glow / border reveal

❌ Symmetric grid with all identical card sizes
   Found: [Y/N — location if found]
   Action: REDESIGN — introduce visual weight variation

❌ Navigation with no scroll behavior change
   Found: [Y/N — location if found]
   Action: ADD — backdrop-blur + border on scroll

❌ Drop shadows using box-shadow with blur > 20px
   Found: [Y/N — location if found]
   Action: REPLACE — use layered sharp shadows or glow

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Slop flags found: [N]
3+ flags = UI layer is rejected. Full redesign required.
1-2 flags = Fix before UI-AGENT proceeds.
0 flags = Proceed to DESIGN-INTEL report.
```

---

### AUDIT DIMENSION 12 — WHAT'S ACTUALLY GOOD

This is not just critique. Document what works.
UI-AGENT must preserve and build on what's already good.

```
STRENGTHS FOUND:
  ✅ [specific element that works well — why it works]
  ✅ [specific element that works well — why it works]
  ✅ [specific element that works well — why it works]

PRESERVE AND EXTEND:
  These elements should be enhanced, not replaced.
  They are the foundation of the design identity.
```

---

## STEP 3 — DESIGN-INTEL REPORT
### The complete brief handed to UI-AGENT.

After STEP 1 (reference education) and STEP 2 (user critique),
produce this report. This is what UI-AGENT receives.
This replaces all generic defaults.

```
╔══════════════════════════════════════════════════════════════╗
║  ZEROSLOP DESIGN-INTEL REPORT                               ║
╠══════════════════════════════════════════════════════════════╣
║  Product:         [name]                                    ║
║  Category:        [detected category]                       ║
║  References used: [3 sites studied]                         ║
║  Mode:            CRITIQUE + ENHANCE / FRESH BRIEF          ║
╠══════════════════════════════════════════════════════════════╣
║  DESIGN IDENTITY                                            ║
║  Aesthetic direction: [one precise phrase]                  ║
║  Not: "clean and modern"                                    ║
║  Yes: "dark-surface precision with amber warmth —           ║
║        like a Bloomberg terminal built by a designer"       ║
╠══════════════════════════════════════════════════════════════╣
║  COLOR SYSTEM (locked — UI-AGENT uses these only)          ║
║  --bg-base:       [value + usage]                           ║
║  --bg-surface:    [value + usage]                           ║
║  --bg-elevated:   [value + usage]                           ║
║  --border:        [value + usage]                           ║
║  --accent:        [value + usage]                           ║
║  --accent-muted:  [value + usage]                           ║
║  --text-1:        [value + usage]                           ║
║  --text-2:        [value + usage]                           ║
║  --text-3:        [value + usage]                           ║
║  --success:       [value]                                   ║
║  --warning:       [value]                                   ║
║  --error:         [value]                                   ║
╠══════════════════════════════════════════════════════════════╣
║  TYPOGRAPHY SYSTEM (locked)                                 ║
║  Display:  [font name] [weight] — headings + hero           ║
║  Body:     [font name] [weight] — paragraphs + UI           ║
║  Mono:     [font name] — code + data values                 ║
║  Scale:                                                     ║
║    Hero:   [size/weight/tracking/line-height]               ║
║    H1:     [size/weight/tracking/line-height]               ║
║    H2:     [size/weight/tracking/line-height]               ║
║    Body:   [size/weight/tracking/line-height]               ║
║    Small:  [size/weight/tracking/line-height]               ║
║    Label:  [size/weight/tracking/line-height]               ║
╠══════════════════════════════════════════════════════════════╣
║  COMPONENT SYSTEM (locked)                                  ║
║  Button primary:  [exact style spec]                        ║
║  Button ghost:    [exact style spec]                        ║
║  Card:            [exact style spec]                        ║
║  Input (default): [exact style spec]                        ║
║  Input (focus):   [exact style spec]                        ║
║  Input (error):   [exact style spec]                        ║
║  Badge:           [exact style spec]                        ║
║  Nav:             [behavior on scroll]                      ║
╠══════════════════════════════════════════════════════════════╣
║  MOTION SYSTEM (locked)                                     ║
║  Page entry:    [fade-up / stagger / none]                  ║
║  Scroll reveal: [trigger + animation]                       ║
║  Hover cards:   [lift px + transition duration]             ║
║  Hover buttons: [behavior + duration]                       ║
║  Duration fast: 150ms — micro-interactions                  ║
║  Duration mid:  250ms — state changes                       ║
║  Duration slow: 400ms — entry / exit animations             ║
║  Easing:        [cubic-bezier values for each type]         ║
╠══════════════════════════════════════════════════════════════╣
║  LAYOUT SYSTEM (locked)                                     ║
║  Max width:     [container width]                           ║
║  Grid:          [column structure]                          ║
║  Section rhythm:[vertical padding scale]                    ║
║  Mobile-first:  [375px breakpoint rules]                    ║
║  Signature element: [the one unforgettable UI moment]       ║
╠══════════════════════════════════════════════════════════════╣
║  WHAT TO PRESERVE FROM EXISTING CODE                        ║
║  ✅ [element to keep and build on]                          ║
║  ✅ [element to keep and build on]                          ║
╠══════════════════════════════════════════════════════════════╣
║  WHAT TO REBUILD                                            ║
║  ❌ [element to replace — specific replacement brief]       ║
║  ❌ [element to replace — specific replacement brief]       ║
╠══════════════════════════════════════════════════════════════╣
║  ANTI-PATTERNS FOR THIS PRODUCT (never use these)          ║
║  ❌ [category-specific slop pattern 1]                      ║
║  ❌ [category-specific slop pattern 2]                      ║
║  ❌ [category-specific slop pattern 3]                      ║
╠══════════════════════════════════════════════════════════════╣
║  DESIGN SCORE (existing code): __/100                       ║
║                                                             ║
║  Color system:      __/20                                   ║
║  Typography:        __/20                                   ║
║  Component quality: __/20                                   ║
║  Motion:            __/15                                   ║
║  Layout:            __/15                                   ║
║  Mobile:            __/10                                   ║
║                                                             ║
║  Slop flags:        [N] found                               ║
║  Verdict: [ENHANCE / PARTIAL REBUILD / FULL REBUILD]        ║
╠══════════════════════════════════════════════════════════════╣
║  UI-AGENT BRIEF                                             ║
║  "Build [product name] using the locked system above.       ║
║   Preserve [X]. Rebuild [Y] and [Z].                        ║
║   The signature moment is [specific element].               ║
║   This should feel like [aesthetic direction]               ║
║   and nothing else."                                        ║
╚══════════════════════════════════════════════════════════════╝
```

---

## DESIGN-SCOUT → UI-AGENT HANDOFF

After the DESIGN-INTEL report is produced:

```
DESIGN-SCOUT COMPLETE.

Design score: [X]/100
Slop flags:   [N] found
Verdict:      [ENHANCE / PARTIAL REBUILD / FULL REBUILD]

Design system locked:
  Colors:     [N CSS variables defined]
  Typography: [font pair confirmed]
  Components: [system defined]
  Motion:     [profile locked]

Handing off to UI-AGENT.
UI-AGENT builds from this brief only.
No defaults. No guessing. No generic.
```

---

## WHAT DESIGN-SCOUT DOES NOT DO

```
❌ Does not make subjective aesthetic judgments ("I prefer...")
❌ Does not suggest trendy designs for the sake of trends
❌ Does not critique things that are genuinely working
❌ Does not produce vague feedback ("make it more modern")
   Every note is specific: what it is, why it's wrong, exact fix
❌ Does not skip the reference study because it "already knows" 
   good design — references are studied fresh for every project
```

---

*zeroslop — 02b-DESIGN-SCOUT*
*Part of the zeroslop methodology: github.com/hotaro6754/ZeroSlop*
