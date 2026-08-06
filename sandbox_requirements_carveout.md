# Verticalized Sandbox — Requirements Carve-Out (Workflow-First Frame)

*Reframing the PRD's A–L pillars around the customer's actual path: friction in Desktop → targeted nudge → guided sandbox → conviction checkpoint → branch to pricing or structured disconfirmation feedback.*

---

## 1. Your model, mapped against what the PRD actually specifies

| Your stage | What you're describing | PRD requirement(s) that cover it | Coverage verdict |
|---|---|---|---|
| **1. Friction occurs** (e.g., invoicing one-by-one instead of batch) | A specific, nameable painful workflow in Desktop | D1 (DT feature-usage signal pipeline) — "friction markers... repetitive manual patterns" | **Partial.** D1 names friction as a signal category but never defines how friction is *measured* (see §3.1) |
| **2. Targeted nudge fires** | The nudge names the specific problem, not just "try QBOA" | C2 (launch trigger library) + D4 (personalized nudge content) | **Covered**, but at a coarser grain than yours — C2's triggers are DT-behavior proxies (batch manual entry → Batch transactions), which is actually close to your example |
| **3. Customer takes the hook → sandbox opens** | Opt-in, enters environment | Pillar C (discovery) → bridge → E1 (orientation) | **Covered** |
| **4. Sandbox is pre-loaded with *that* workflow + a how-to** | Not a generic vertical tour — the specific feature that solves *their* friction, with a walkthrough | D3 (personalized "features to try" panel) + F1 (interactive per-feature tours) + F3 (DT-vs-ADV contrast framing) | **Covered in principle**, but D3/F1 default to vertical-curated content with personalization as a ranking layer on top — not a friction-triggered, single-feature deep-link as the *default* entry. C5 (deep-link into the aha) is the closest match and it's **P1, not P0** |
| **5. Conviction checkpoint** | An explicit "are you convinced?" moment before branching | Not named as such. E5 (sitting-end/window-end moments) and F7 (micro-conversion prompts) are the closest analogues | **Gap** — see §3.3 |
| **6a. Convinced → pricing/questions** | Move to commercial conversation | J1 (talk-to-sales), J2 (pricing path) | **Covered** |
| **6b. Not convinced → structured feedback on expectation-vs-actual delta** | Capture *why* it didn't land, feed it back as product signal | J4 (not-yet path) records suppression only; H4 tags support contacts | **Gap** — see §3.4 |

The headline: your model is **workflow-first** — one friction, one feature, one proof point. The PRD's own Principle 3 ("verticalization is a means, not the point... a business like mine") actually agrees with this. But the *implementation* defaults to **vertical-first with personalization layered on** (industry template is P0 core; the friction-to-feature deep-link that would make your flow the default path is P1/fast-follow, not launch). That's a real tension between the PRD's stated principle and its phasing — worth naming explicitly if you're pushing this framing upstream.

---

## 2. Requirements carved out by your stage (holistic list, PRD IDs cross-referenced)

### Stage 1 — Friction detection
- D1 DT feature-usage signal pipeline (P0)
- D2 DT→ADV feature mapping, PMM-owned (P0)
- L1 Privacy review gating D1's use of telemetry (P0, blocking)
- **Not specified:** a severity/cost measure for friction (time lost, workaround steps, error rate) — D1 only says "friction markers," no scoring method

### Stage 2 — Targeted nudge
- C1 Trigger framework (server-side configurable) (P0)
- C2 Launch trigger library, hypothesis + target conversion per trigger (P0)
- C3 Frequency capping / suppression (P0)
- C4 Trigger-level economics + kill criteria (P0)
- D4 Personalized nudge content (P0)
- C7 Accountant-aware suppression (P1)

### Stage 3 — Hook taken, sandbox opens
- B2 Confidence-based routing (P0)
- B3 Customer-facing industry choice/override (P0)
- E1 Orientation moment (P0)
- C5 Deep-link into the aha, bridge-skippable for nudge entries (**P1** — this is the piece that would make your flow the default, and it's deferred)

### Stage 4 — Guided proof of the specific fix
- D3 Personalized features-to-try panel (P0)
- F1 Interactive per-feature tours (P0)
- F3 DT-vs-ADV contrast framing (P0)
- F2 Tour content system (P0)
- E4 DT-familiar wayfinding (**P1**)
- F5 In-sandbox AI guide (**P1**, scope TBD)

### Stage 5 — Conviction checkpoint
- **No dedicated requirement.** Closest existing hooks:
  - E5 sitting-end moment (summarizes what was toured, offers CTAs)
  - F7 micro-conversion prompts at tour completion
  - Neither asks "did this solve your problem" — both assume tour completion = value delivered

### Stage 6a — Convinced path
- J1 Talk-to-sales (carried from pilot, P0)
- J2 Pricing path (P0)
- D6 Seller-visible usage context on the lead (P1)
- D7 Gap honesty — don't oversell where ADV has no equivalent (P1)

### Stage 6b — Not-convinced path
- J4 Not-yet path (P1) — records "remind me later / don't contact," no reason capture
- H4 Feedback loop to product (P1) — tags *support* contacts, not declined-conviction contacts
- **No requirement captures the expectation-vs-actual delta at the point of decline.**

---

## 3. Where the PRD asserts rather than substantiates

### 3.1 Friction is conflated with frequency
D1 groups "top capabilities by frequency" and "friction markers" in the same signal pipeline without separating them. Frequency and friction aren't the same thing — a workflow can be used constantly and be fine, or used rarely and be genuinely painful. D3's badge copy ("*Because you use job costing in Desktop*") is a frequency claim wearing a friction-relief costume. Nothing in the PRD defines a friction metric independent of usage count. Your batch-invoicing example actually works because it's *both* frequent and slow — but the PRD's pipeline as written would surface it on frequency alone, and could just as easily badge a frequent-but-painless workflow with the same confident framing.

### 3.2 The "aha" is defined by assertion, then measured against itself
E2 requires each template to *name* its target aha (e.g., "live job profitability in one click"). Certification (A2) checks that the *feature path works* — not that customers actually experience it as an aha. Then §5's success metrics track "% of windows reaching the vertical's designated aha moment" — which is circular: it measures adherence to an assumed aha, not whether that assumed aha is the customer's actual aha. There's no step where the aha claim is validated against real customer reaction *before* it's baked into a certified template and a success metric.

### 3.3 Personalization's core bet ships before it's tested
D5 (A/B personalized panel vs. vertical-default) is the one requirement that would actually tell you whether "personalization earns its complexity" — and it's **P1, fast-follow**, not gating. That means the entire D-pillar (P0) ships into production carrying an unvalidated assumption that usage-based personalization beats generic vertical defaults. Q4 in the open-questions table names this directly ("if personalized panels/nudges don't beat vertical defaults, cut the D-pillar's ongoing cost") — the PRD itself flags this as unresolved, but the phasing doesn't block on resolving it first.

### 3.4 No mechanism for capturing disconfirmation
This is the gap your model surfaces most clearly. When a customer goes through the sandbox and *isn't* convinced, the PRD has:
- a way to suppress future contact (J4)
- a way to tag it if it generates a support ticket (H4)

It has no requirement to ask the customer what they expected vs. what they got. That delta is exactly the signal that would tell you whether the aha claim (3.2) or the personalization bet (3.3) is actually working, per vertical, per feature. Right now the only failure signal the PRD collects is behavioral (didn't convert, didn't return) — not explanatory.

---

## 4. Requirements worth proposing (not in the PRD as written)

1. **Friction-severity scoring** — extend D1 so friction markers carry a measured cost (time, steps, error rate), not just a co-located frequency count. Without this, "personalized" nudges default to "frequent," not "painful."

2. **Pre-certification aha validation** — before a template is certified (A2), validate the named aha (E2) against actual customer reaction (even lightweight — a handful of moderated sessions), not just that the feature path executes. Otherwise certification checks the *mechanism*, not the *moment*.

3. **Conviction checkpoint as a designed moment** — an explicit, honest "did this solve it for you?" beat at the natural end of a guided tour (extends F1/F7), distinct from the passive sitting-end summary in E5. This is the hinge your model puts weight on and the PRD currently doesn't name.

4. **Disconfirmation feedback capture** — when a customer declines to proceed (J4) or the window resets without conversion, capture structured expectation-vs-actual input: what they thought QBOA would fix, what it actually showed them, where the gap was. Feed this to the same loop H4 uses for support contacts, but as its own category — it's a product-quality signal, not a support-quality one.

5. **Friction-to-feature deep-link as a first-class path, not fast-follow** — promote C5 (or a variant scoped to your model) toward P0 if the goal is genuinely workflow-first per Principle 3. As phased, the vertical-template path is the load-bearing P0 default and the friction-specific path is an enhancement — which undercuts the principle it's meant to serve.

---

## 5. Evidence from the pilot panel (Construction, "Test drive")

The actual pilot artifact for the D3/F1 panel confirms several of the gaps above concretely rather than hypothetically:

- **Cards are vertical-generic, not friction-personalized.** Five features (Estimates/Proposal, WIP reporting, AIA-style invoices, Batch entry, Spreadsheet Sync) are shown identically to every Construction customer with benefit-framed copy ("Save hours by creating or updating large sets of invoices..."). None reference the customer's own Desktop behavior. This is the D3 *fallback* state (per PRD: "vertical defaults after" personalized picks) — meaning the panel as built and shown is running the un-personalized path, with no visible badge state for the personalized one.
- **Batch entry is present and matches your example exactly** — confirming the feature-to-friction mapping (D2) already exists for this case. The gap isn't feature coverage; it's that the card doesn't know (or show) that *this* customer was invoicing one at a time.
- **Tours render as static instruction text, not interactive coach-marks.** F1 specifies "do-it-with-me walkthroughs... over the live seeded environment." What's shown is a written three-step instruction under each card. Worth confirming whether this is a placeholder/lo-fi state or the intended pilot fidelity — if the latter, F1 as specified isn't yet built.
- **No progress/checklist state (E3) visible** — no "N of 5 tried" marker, no visual differentiation of a completed card.
- **No conviction checkpoint and no disconfirmation path.** The panel's only two exits are *Get Advanced* and *Talk to sales*. There's no third option for a customer who read all five cards and wasn't convinced — confirming §4.4's gap isn't just absent in the requirements doc, it's absent in the built experience. A customer who churns out silently here leaves no signal beyond "didn't convert."
- **No window chrome ("Day X of 7," re-entry framing) visible in this surface** — may be elsewhere in the flow; worth confirming E8's chrome actually persists onto this panel specifically, since it's a likely place for a customer to lose track of the window.

## 6. Top-5 pain-point hub model — discovery hook + the other four

Proposed structure: lead the nudge and FTU with the *one* pain point that fired detection, then surface the vertical's other four candidate pains as a visible menu — rather than either (a) a single-feature nudge with nothing else to explore, or (b) a flat five-card list with no personalized entry point (which is what the pilot panel in §5 currently is).

**Why this is the right shape**
- Solves the breadth-vs-personalization tradeoff: the hook gives "this solves *my* problem," the other four give "a business like mine, comprehensively" (Principle 3) — without needing five separate detection events per customer.
- Matches window pacing better than trying to build confidence on all five in one sitting: **deep guided tour on the hook pain** (full F1 treatment, ~3 min) + **lightweight preview cards for the other four** (headline value only) + **checklist (E3) tracking what's left**, which becomes the return-visit hook ("2 of 5 explored — come back for WIP reporting"). This is Principle 1's "window rewards the return" operationalized.

**Tension with the PRD as written**
E2 assumes **one named aha per vertical** (e.g., Construction: live job profitability in one click). This model implies the aha is **customer-specific** — whichever of the top-5 pains fired the nudge *is* that session's aha, and the vertical's canonical aha is just one candidate among five. E2 would need rewording from "the vertical's aha" to "top-5 candidate ahas per vertical, selection logic per customer" — a small wording change with a real implication: certification (A2) now has to validate five paths per template, not one.

**Feedback taxonomy for this model** — tie decline reasons to the same five-pain taxonomy rather than generic categories, so responses are diagnostic (which pain, which feature) rather than just descriptive. See §7's choice-card set, which reuses this structure.

---

## 7. Abandonment segmentation & post-trial feedback framework

Not every non-conversion is the same failure, and treating them identically either annoys an engaged evaluator with a survey they don't need, or lets a confused-but-still-trying customer walk out the door when a small nudge would have kept them going. Three segments, classified by behavior, each with a different response:

### The usage matrix (classification signals)

| Signal | What it indicates |
|---|---|
| Time-to-first-action | Long delay before any click = hesitation, not disinterest |
| Dropdown/instruction opened without follow-through | Found the instruction, didn't trust it enough to act |
| Idle time mid-tour | Stalled partway through a guided step |
| Cards expanded vs. cards tried | Browsing without doing = orientation problem |
| Session length + tour completions | Low on both = busy; high on either = evaluating |
| Return visits within window | A second visit after a stall = still interested, still stuck |

**Classification rule:** hesitation signals present (stall, opened-not-followed) → *lost/unfamiliar*, regardless of session length. Hesitation signals absent + short session + near-zero card expansion → *busy/low patience*. Tour completions, multiple cards tried, or a return visit → *serious evaluator*, even if they ultimately decline.

### Segment 1 — Lost / unfamiliar: rescue, don't survey
- **Trigger:** stall mid-tour, or instruction opened without the next click within N seconds.
- **Response:** a small, dismissible in-context prompt — *"Looks like you're exploring — want a walkthrough?"* — launching the guided tour (F1) or AI guide (F5) at the exact step they stalled on. Never modal, never blocking.
- **If declined again:** don't ask twice in one session. Passively tag the session "needs orientation" from behavior alone — this feeds E4 (DT-familiar wayfinding); a cluster of this tag on one template/feature signals the tour content is unclear, not that the customer is uninterested.
- **Do not fold this into the disconfirmation survey** — asking "why didn't you continue" of someone still mid-attempt reads as premature and can push them out.

### Segment 2 — Busy / low patience: capture sentiment, don't spend their attention
- **No in-session ask, ever** — if they didn't engage enough to get lost, a survey is just the second thing they bounce off.
- **Defer to the post-reset email (I1), single tap, no explanation required:** *"Was this a bad time?"* → *Remind me later* / *No thanks*. No free text.
- **Route to trigger economics (C4), not the product feedback loop (H4).** A cluster of "busy" tags on one trigger is a targeting/timing problem, not evidence the sandbox itself failed — mixing it into the serious-evaluator feedback stream dilutes the signal that actually says something about the product.

### Segment 3 — Serious evaluator: the real feedback
- **Trigger:** explicit decline (clicked past the panel without converting) or window expiry after crossing the serious-evaluator engagement threshold.
- **Choice cards, tied to the pain-point taxonomy from §6** (diagnostic, not just descriptive):
  - *"[Feature] didn't work the way I actually do it"*
  - *"I didn't see how this saves me time or money"*
  - *"Something I need wasn't there"*
  - *"Cost is a concern"*
  - *"Just exploring — not ready yet"*
  - *"Other"* + free text
- **One screen, no required fields, skippable** — extends F7's "never modal-blocking" principle to this ask.
- **Gap-flagged responses route to CS/sales as a lead heads-up** (extends D7's gap-honesty principle) — the seller shouldn't get ambushed by a gap the customer already told the product about.
- **Feed to H4 as its own tagged category**, distinct from support-ticket-driven feedback — this is product-quality signal, not support-quality signal.

### New requirements this adds to §4's list
6. **Usage-matrix classification** — a lightweight behavioral scoring pass (hesitation signals + engagement depth) run at session-end/window-end, gating which of the three response tracks fires. Sits upstream of E5/F7/J4 and determines which one actually executes.
7. **Segment-appropriate response routing** — the three tracks above, wired to distinct destinations (E4 orientation feedback / C4 trigger economics / H4 product feedback) rather than one undifferentiated "not-yet" path (J4 as currently written).

---

## 9. Multi-persona expansion — accountant and sales channels

Expanding provisioning beyond self-serve BIZ customers to ProAdvisors/accountants and the internal sales team isn't a UI tweak — it changes where personalization signal comes from and how outcomes get recorded, for each channel:

| | Customer (current) | Accountant | Sales |
|---|---|---|---|
| **Provisioning entry** | In-product nudge (C1–C2) | "Provision for client" action in accountant console, likely batched | From CRM, during/after discovery call |
| **Personalization signal** | D1 telemetry | Accountant's own client knowledge — needs a manual override input | Discovery-call notes — structured, not behavioral |
| **Management surface** | Single-window chrome (E1/E8) | Multi-sandbox dashboard (status per client) — **not specified anywhere in the PRD** | Multi-sandbox dashboard, CRM-integrated |
| **Exit CTA** | *Get Advanced* / *Talk to sales* (J1/J2) | *Recommend to client* / *Schedule migration* | *Mark opportunity stage* / *Escalate* |
| **Reasoning capture** | In-app choice cards (§7) | Structured outcome field in accountant dashboard | CRM closed-lost reason code |

**Requirements this surfaces that don't exist in the PRD:**
- Manual pain-point selection input, feeding the same D3/E2 pipeline telemetry currently feeds — needed for both accountant and sales channels.
- Multi-sandbox dashboard/list view — a new surface, not a variant of E1/E8.
- **Role-aware framing (E7)** — flagged as unresolved/deferred in the original PRD — becomes non-optional once three personas share the same underlying flow.
- RBAC scoping for accountant visibility into client telemetry (least-privilege question — should the accountant see real DT data, or only vertical defaults).
- L4's "don't enter real data" deterrence copy needs an update for the case where someone other than the account owner is driving the session — consent for accountant-initiated sandboxes isn't covered as written.

**Measurement requirements:**
- **A single lifecycle ID that survives channel handoffs** — a lead may originate in Salesforce, the sandbox lives in QBOA infrastructure, and the outcome conversation may happen on a call that touches neither system. Without one ID, the three channels produce three funnels that don't reconcile.
- **Initiator as a first-class field on every event** — "serious evaluator" engagement means something different from a self-serve customer vs. a sales rep clicking through their own demo; conflating the two overstates customer intent.
- **One shared outcome taxonomy across three input surfaces** — self-serve choice-cards, accountant dashboard field, and CRM loss-reason code all need to map to the same categories (reusing §6/§7's pain taxonomy), or channel comparison becomes manual spreadsheet reconciliation.
- **Report channels separately, don't blend into one adoption rate** — CRM-sourced outcomes are self-reported and softer than behavioral telemetry (a rep under pipeline pressure has some incentive to round favorably); keep lanes distinct until volume validates consistency.
- **Decide churn attribution for the accountant channel up front** — if an accountant recommends the sandbox and the client later churns, is that a product failure or an advisor-recommendation failure? Worth coding this before volume makes it a retroactive dispute.

---

## 10. Roadmap reality check — Aug'26 rollout data (source: DT R4 profile pivot, filtered R4ADV/Single Entity/No Payroll/No Accountant)

The roadmap data (Test Drive Go-Live dates by vertical) reframes prioritization from count-based to readiness-based. Four roadmap columns matter: *Smart Parity*, *Feature Parity*, *Data Seeding Available*, *Test Drive Go-Live*. **Construction is the only vertical with all four dated.** Every other vertical has Feature Parity and Data Seeding blank — including the five with a Test Drive Go-Live date **this month**.

| Tier | Verticals | Companies | % of base |
|---|---|---|---|
| **0 — Live** | Construction | 5,370 | 7.5% |
| **1 — Test Drive committed for Aug'26** | Professional Services, Manufacturing, Field Services, Healthcare, Non-Profit | 22,220 | 31.1% |
| **2 — Smart Parity ready, no Test Drive date** | Admin & Support, Personal & Maintenance, Real Estate, Financial Services, Transportation, Media & Telecom, Restaurants, Arts & Entertainment, Education, Accommodation, Mgmt of Companies, Utilities | 18,455 | 25.8% |
| **3 — Smart Parity itself delayed to Nov'26** | Retail & E-Commerce, Wholesale, Agriculture, Government, Mining/Oil/Gas, Unspecified | 25,442 | 35.6% |

**Anomalies worth surfacing to whoever owns sequencing:**
- **Admin & Support Services** (#2 by volume, 8%) has no Test Drive date, while **Non-Profit** (4%, a quarter its size) already does — either a deliberate heterogeneity call (§6's sub-segmentation risk playing out) or an unexplained gap.
- **Retail & E-Commerce** (#5 by volume, 6%) has Smart Parity itself delayed to Nov'26 — no UX work pulls this forward; it's gated upstream.
- **Unspecified** (23% of the entire base, larger than any single named vertical) has only a Nov'26 Smart Parity date and no Test Drive row at all — confirms §6's fallback-hub proposal is necessary, not optional, since there's no industry to template against.

**The near-term risk:** the blank Feature Parity/Data Seeding columns for all five Tier 1 verticals mean the Go-Live date has content risk underneath it. If those five ship using Construction's current fallback state (§5 — generic vertical-default cards, no personalization badge, no conviction checkpoint), the gaps documented there get reproduced five times simultaneously instead of fixed once.

---

## 11. UX priority list, mapped against PRD sections

For communicating trade-offs and negotiating scope, ordered from launch-blocking to next-phase, each tied to its PRD reference:

| # | Priority tier | Item | PRD section(s) | Current status | Why it matters now |
|---|---|---|---|---|---|
| 1 | **Blocking** | Reusable hub shell across verticals (not five bespoke builds) | D3, F1, F2, F3 | Built once for Construction (§5); not yet confirmed as a shared shell | Makes five simultaneous Aug'26 launches feasible at all |
| 2 | **Blocking** | Per-vertical feature mapping + panel content | D2, D3 | Blank in roadmap (Feature Parity column) for all Tier 1 verticals | This is the actual content gap behind the Go-Live dates |
| 3 | **Blocking** | Per-vertical tour content | F1 | Blank in roadmap; Construction's own tours are static text, not interactive (§5) | Tour fidelity is the "explain it without an agent" mechanism |
| 4 | **Blocking** | Data seeding closure per vertical | A1 (implied), Data Seeding column | Blank for all Tier 1 verticals | No seeded data, no sandbox to try — most concrete risk on the roadmap |
| 5 | **Critical, cheap once built** | Progress/checklist state | E3 | Absent from pilot panel (§5) | Prevents silent loss across all five verticals at once, not just Construction |
| 6 | **Critical, cheap once built** | Conviction checkpoint before exit CTAs | Not named in PRD (§3.3, §4.3) | Gap | One build, inherited by all five templates simultaneously |
| 7 | **Critical, cheap once built** | Disconfirmation feedback capture, tied to pain taxonomy | Extends J4, H4 (§7, §4.4) | Gap | Only way to know if any of the five new templates is failing, without waiting a full cycle to find out |
| 8 | **Important, weeks-out** | Friction-severity scoring | Extends D1 (§3.1) | Gap | Matters once D3 personalization actually turns on (hasn't yet, per §5) |
| 9 | **Important, weeks-out** | DT-familiar wayfinding content | E4 | P1 in PRD | Raises tour quality; not launch-blocking |
| 10 | **Important, weeks-out** | Lightweight aha validation per new template | Extends A2, E2 (§4.2) | Gap; full version too slow for this timeline | Retroactive spot-check beats no validation at all |
| 11 | **Important, weeks-out** | D5 personalization A/B test | D5 | P1, fast-follow in PRD | Sequence after personalization is live, not before |
| 12 | **Good to have** | In-sandbox AI guide | F5 | P1, scope TBD in PRD | No reason to pull forward |
| 13 | **Good to have** | Friction-to-feature deep-link as default entry | C5 (§4.5) | P1 in PRD | Correct long-term shape; current nudge mechanism works well enough not to block on it |
| 14 | **Good to have** | Role-aware framing / multi-persona expansion | E7; new requirements in §9 | Deferred in PRD | Real, but a separate initiative with its own lifecycle-ID and RBAC questions |
| 15 | **Good to have** | Unspecified vertical-agnostic fallback hub | New requirement (§10) | Gap | Real at 23% of base, but can't be rushed into an Aug'26 vertical-template cycle |

---

## 12. One structural note for framing this upward

If you're taking this to whoever owns the BRD next revision: the strongest version of your critique isn't "the PRD is wrong" — it's "the PRD's own Principle 3 already states your model as the goal, but the P0/P1 phasing and the certification process (A2) don't yet operationalize it that way." That's a much easier gap to close than a disagreement about direction, since the phasing is explicitly marked TBD/open in several places (Q1, Q4, dependency 2) rather than settled.
