# Product Management Assistant — Worked Examples

**Companion file to `Product-Management-Assistant.md`.** Upload both files together in the same ChatGPT-5 conversation. This file holds fuller worked examples for the 7 newer skills (Cards 11-17: Metrics Review, Product Brainstorming, Roadmap Update, Sprint Planning, Stakeholder Update, Epic Hypothesis, Epic Breakdown Advisor). The main file's cards reference this file by name when a fuller example helps — this file is not required to use those cards, it just shows one fully worked instance of each.

**Note on scope:** Cards 1-10 (the original 10 director-level documents) do not have entries here — their examples live inline in the main file as before. This file is additive, for the 7 new skills only.

---

## Example: Card 11 — Metrics Review

**Scenario:** Monthly metrics review for a B2B SaaS project management tool, 8 months post-launch.

### Summary
Overall product health is improving but retention is the weak point. WAU grew 18% month-over-month, but D30 retention dropped from 52% to 44% — the second consecutive month of decline. Activation rate is strong at 61%. Recommend investigating the retention drop before next month's review; it's the one metric moving the wrong direction.

### Metric Scorecard

| Metric | Current | Previous | Change | Target | Status |
|---|---|---|---|---|---|
| WAU | 4,200 | 3,560 | +18% | 4,000 | On track |
| Activation rate | 61% | 58% | +3pp | 55% | On track |
| D30 retention | 44% | 52% | -8pp | 55% | At risk |
| NRR | 108% | 106% | +2pp | 110% | On track |
| Support tickets/week | 34 | 22 | +55% | <30 | At risk |

### Trend Analysis
**D30 retention (44%, down from 52%):** Two-month decline. Correlates with the support ticket spike — both started the week after the v2.3 workspace redesign shipped. Segment breakdown shows the drop is concentrated in accounts with 3+ users (team accounts), not solo accounts. This suggests the redesign broke something in team collaboration flows specifically, not onboarding broadly.

**Support tickets (34/week, up from 22):** Same timing as the retention drop. Top ticket category: "can't find my team's shared workspace" — consistent with the collaboration-flow hypothesis above.

### Bright Spots
- WAU growth (18%) beat target for the second month running
- Activation rate at 61% is the highest since launch — onboarding changes from two months ago are working

### Areas of Concern
- D30 retention declining for team accounts specifically, correlated with the v2.3 redesign
- Support ticket volume up 55%, concentrated in one category (shared workspace navigation)

### Recommended Actions
- **Investigate immediately:** pull 10 team-account churned users from this cohort, check if they hit the "can't find shared workspace" issue before churning
- **Experiment:** ship a workspace navigation fix as a fast-follow patch, re-measure D30 retention on the next cohort in 4 weeks
- **Alert:** set a threshold alert on support ticket category volume so a spike like this triggers review sooner next time

### Context and Caveats
- D30 retention for the affected cohort won't fully resolve for another ~2 weeks (still inside the 30-day window)
- Solo-account retention is unaffected — this narrows the fix scope to team/collaboration surfaces only

---

## Example: Card 12 — Product Brainstorming

**Scenario:** A sample conversation transcript showing the Frame → Diverge → Provoke → Converge flow (Problem Exploration mode). This is not a document deliverable — it's how the conversation itself should feel.

**User:** "Our free-to-paid conversion has been flat at 3% for two quarters. I think we need better upgrade prompts in the app."

**Assistant (Frame):** "Before we jump to prompts — what have you tried already, and what have you learned? And when you say 'flat,' is that flat in absolute numbers or flat as a percentage of a growing free base?"

**User:** "Flat as a percentage. We've tried a banner at the top of the dashboard, that's it."

**Assistant (Provoke — solutioning before framing):** "That's actually a useful signal, but I want to push back before we design prompt #2. 'Better prompts' assumes the problem is *visibility* of the upgrade path. What if the real problem is that free users don't hit the point where they'd actually want to pay? What happens today, concretely, when a free user hits a plan limit — do they get blocked, degraded, or nothing?"

**User:** "They just... get a small warning. Nothing blocks them."

**Assistant (Diverge):** "That's worth sitting with. If nothing forces the moment of 'I need to upgrade,' more prompts just add noise to people who have no reason to click. Let's generate a few genuinely different directions before deciding: (1) make limits actually bind, so hitting them creates real friction; (2) find the segment of free users closest to a limit and target *only* them, rather than blasting everyone; (3) do the opposite of prompting — remove the limit entirely for a segment and see if usage growth predicts later willingness to pay; (4) look at what free users do right before they'd naturally want a paid feature (inviting a 6th teammate, say) and prompt exactly there, not on a dashboard banner unrelated to intent."

**User:** "I like #2 and #4 together."

**Assistant (Converge):** "That's a real direction — targeted, intent-based prompting instead of broad awareness prompting. Riskiest assumption in that combo: that free users are actually *aware* they're near a limit at all. Cheapest test: pull 15 free accounts near a limit, manually message them the exact same thing your best prompt would say, see if any convert without touching the product at all. If that doesn't move anyone, the banner redesign was never going to work either — the problem isn't the prompt, it's whether limit-proximity actually predicts intent to pay."

---

## Example: Card 13 — Roadmap Update

**Scenario:** Before/after reprioritization on a Now/Next/Later roadmap, triggered by a large customer's churn risk.

### Before
```
Now:
- Bulk export (CSV/PDF) — On Track — Sarah — Q1
- Mobile push notifications — On Track — Dev — Q1

Next:
- SSO for enterprise — Not Started — TBD — Q2
- Custom fields — Not Started — TBD — Q2

Later:
- API v2 — Directional — TBD — Q3+
```

### What changed
Our largest enterprise account ($180K ARR, renewal in 6 weeks) flagged SSO as a blocker for renewal during a QBR call this week. Previously SSO was a "nice to have" for Q2; it's now a renewal-blocking requirement with a hard deadline.

### After
```
Now:
- SSO for enterprise — In Progress — Sarah — 5 weeks (moved up from Next; renewal-blocking)
- Bulk export (CSV/PDF) — At Risk — Dev — Q1 (deprioritized to make room for SSO)

Next:
- Mobile push notifications — Not Started — TBD — Q2 (moved down from Now)
- Custom fields — Not Started — TBD — Q2

Later:
- API v2 — Directional — TBD — Q3+
```

### Changes This Update
- **SSO moved Next → Now:** driven by a renewal-blocking requirement from a $180K account, hard deadline in 5 weeks
- **Bulk export moved to At Risk:** Sarah is now on SSO; bulk export loses its owner and its Q1 target is no longer realistic without adding capacity
- **Mobile push notifications moved Now → Next:** deprioritized to free up Dev's time as a potential second engineer on SSO if needed

**What comes off:** bulk export's Q1 delivery is the direct tradeoff for taking on SSO at this urgency. This was surfaced explicitly to the team, not absorbed silently.

---

## Example: Card 14 — Sprint Planning

**Scenario:** A fully filled sprint plan for a 4-person team, 2-week sprint, following the Card 14 template exactly.

```markdown
## Sprint Plan: Sprint 24 — Workspace Navigation Fix
**Dates:** Aug 4 — Aug 15 | **Team:** 4 engineers
**Sprint Goal:** Ship the workspace navigation fix that's driving the D30 retention drop, and validate it resolves the support ticket spike.

### Capacity
| Person | Available Days | Allocation | Notes |
|--------|---------------|------------|-------|
| Priya | 10 of 10 | 8 points | — |
| Marcus | 7 of 10 | 5 points | 3 days PTO mid-sprint |
| Dana | 10 of 10 | 8 points | On-call this sprint, -1 pt buffer applied |
| Leo | 10 of 10 | 8 points | — |
| **Total** | **37 of 40** | **29 points** | |

### Sprint Backlog
| Priority | Item | Estimate | Owner | Dependencies |
|----------|------|----------|-------|--------------|
| P0 | Fix shared workspace navigation (root cause from metrics review) | 8 pts | Priya | None |
| P0 | Add workspace breadcrumb for team accounts | 5 pts | Leo | Blocked by navigation fix landing first |
| P1 | Regression test suite for workspace flows | 5 pts | Dana | None |
| P1 | Support ticket triage — clear backlog from v2.3 spike | 3 pts | Marcus | None |
| P2 | Workspace search (stretch) | 8 pts | Leo | None |

### Planned Capacity: 29 points | Sprint Load: 29 points (100% of capacity — no buffer, flagged below)

### Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| Sprint load is at 100% capacity, no buffer | Any interrupt pushes P1/P2 out | If an interrupt lands, cut the stretch item (workspace search) first |
| Breadcrumb work blocked on navigation fix landing early | Leo idle if Priya's fix slips past day 3 | Leo picks up support ticket triage as backup work if blocked |

### Definition of Done
- [ ] Code reviewed and merged
- [ ] Tests passing (including new regression suite)
- [ ] Documentation updated (if applicable)
- [ ] Product sign-off — confirm with a sample of previously-affected team accounts

### Key Dates
| Date | Event |
|------|-------|
| Aug 4 | Sprint start |
| Aug 8 | Mid-sprint check-in |
| Aug 15 | Sprint end / Demo |
| Aug 16 | Retro |
```

**Note the flagged risk:** this plan is deliberately shown at 100% capacity (not the recommended 70-80%) to illustrate what the "Risks" section should catch when planning goes over the safe threshold — the sprint-planning card's own tip ("leave buffer") would normally push this backlog down to ~23 points, cutting the stretch item before the sprint even starts.

---

## Example: Card 15 — Stakeholder Update

**Scenario:** The same underlying situation (SSO pulled forward for a renewal-blocking customer) told three different ways, to show how audience changes the shape — not the facts.

### Executive / Leadership version
```
Status: Yellow

TL;DR: We pulled SSO forward to save a $180K renewal; bulk export slips as the tradeoff.

Progress:
- SSO now in active development, targeting delivery in 5 weeks to meet the renewal deadline
- Enterprise renewal conversation is unblocked pending SSO delivery

Risks:
- Bulk export (originally Q1) is now at risk with no clear new date. Mitigation: re-plan once SSO ships.

Decisions needed:
- None this week — direction is set, executing.

Next milestones:
- SSO beta with the affected customer — Aug 25
```

### Engineering version
```
Shipped:
- Nothing new this week — sprint just kicked off with re-prioritized scope

In progress:
- SSO for enterprise — Sarah. Targeting 5-week delivery. No blockers currently.
- Workspace navigation fix — Priya. On track, landing by mid-sprint.

Decisions:
- Bulk export deprioritized this sprint to free capacity for SSO. Rationale: renewal-blocking requirement from a $180K account, hard deadline.

Priority changes:
- SSO moved from Next → Now. Bulk export moved from Now → At Risk (owner reassigned).

Coming up:
- Once SSO ships, re-plan bulk export delivery date with the team.
```

### Customer / External version (for the affected customer specifically, not a broad announcement)
```
What's new:
- Single Sign-On (SSO) support is in active development and on track for your renewal timeline.

Coming soon:
- Beta access to SSO — expected week of Aug 25. We'll reach out directly to set up your team's testing.

Known issues:
- None blocking at this time.

Feedback:
- Your CSM will coordinate the beta testing window directly with your team.
```

**What stayed constant across all three:** the underlying facts (SSO pulled forward, bulk export slipped, 5-week timeline, $180K account). **What changed:** altitude, jargon, and what's asked of the reader — executives get a risk flag and no ask, engineers get the "why" behind the reprioritization, the customer gets zero internal detail and a concrete next step for them specifically.

---

## Example: Card 16 — Epic Hypothesis

**Scenario:** Three examples — two good, one bad — showing the quality bar for each section, drawn from the source skill's own illustrations.

### Good example 1
```markdown
### If/Then Hypothesis
**If we** add one-click Google Calendar integration
**for** trial users managing multiple meetings
**Then we will** increase activation rate from 40% to 50% within 30 days

### Tiny Acts of Discovery Experiments
**We will test our assumption by:**
- Building a clickable Figma prototype of the calendar-connect flow, testing with 8 trial users
- Manually connecting calendars for 10 new trial signups this week and tracking their activation

### Validation Measures
**We know our hypothesis is valid if within 4 weeks we observe:**
- Activation rate increases from 40% to 50% (quantitative)
- 75% of surveyed trial users say the integration saved them time (qualitative)
```
**Why this works:** the "if we" is a specific action, the persona is narrow enough to be meaningful, the outcome is a number with a baseline and a deadline, and the experiments are genuinely cheap (a prototype and a manual concierge test, not a full build).

### Good example 2
```markdown
### If/Then Hypothesis
**If we** provide bulk delete functionality
**for** power users managing 1,000+ items
**Then we will** reduce time spent on cleanup tasks by 70%

### Tiny Acts of Discovery Experiments
**We will test our assumption by:**
- Adding a "Request bulk delete" button to the UI and measuring click-through rate over 2 weeks
- Manually running bulk-delete requests for 5 power users who ask for it, timing how long it actually saves them

### Validation Measures
**We know our hypothesis is valid if within 3 weeks we observe:**
- At least 15% of power users click the request button (quantitative signal of real demand)
- The 5 manually-served users report meaningful time savings in a follow-up interview (qualitative)
```

### Bad example (what to avoid — and why)
```markdown
### If/Then Hypothesis
**If we** build a dashboard
**for** users
**Then we will** have a dashboard
```
**What's wrong:** "build a dashboard" is a feature, not an action tied to a problem. "For users" isn't a persona — it's everyone, which is no one in particular. "We will have a dashboard" is an output, not an outcome — it describes what gets shipped, not what changes for the user or the business. This hypothesis is unfalsifiable: there's no way to be wrong about it, which means it isn't testing anything.

**The fix, applying the quality bar:** "If we build a dashboard showing real-time task status, for project managers coordinating 3+ person teams, then we will reduce time spent asking teammates for status updates by 50% within 3 weeks."

---

## Example: Card 17 — Epic Breakdown Advisor

**Scenario:** Four worked examples reproduced from the source skill, since they're genuinely illustrative of how the 9-pattern sequence plays out differently depending on what the epic actually looks like.

### Example 1 — Pattern 1 applied (Workflow Steps, thin end-to-end)

**Epic:** "Publish blog post (requires editorial review, legal approval, staging)"

**Pre-Split Validation:** ✅ Passes INVEST

**Pattern 1 check:** "Does this have workflow steps?" → YES

**❌ Wrong split (step-by-step):**
1. Editorial review story
2. Legal approval story
3. Publish story

Problem: Story 1 alone delivers nothing — no post goes live until story 3 ships.

**✅ Right split (thin end-to-end):**
1. **Publish post (simple path)** — author uploads, post goes live immediately, no reviews at all
2. **Add editorial review** — post now waits for editor approval before going live
3. **Add legal approval** — post waits for legal + editorial before going live

**Why this works:** every story delivers the *full* workflow, just with increasing sophistication layered on top.

### Example 2 — Pattern 2 applied (CRUD Operations)

**Epic:** "Manage user profiles"

**Pattern 2 check:** "Does this say 'manage'?" → YES (signals bundled CRUD)

**Split:**
1. Create user profile
2. View user profile details
3. Edit user profile info
4. Delete user profile

**Split Evaluation:**
- ✅ Reveals low-value work: after analysis, "Delete profile" turns out to be rarely used → candidate to deprioritize
- ✅ Equal-sized stories: each roughly 1-2 days

### Example 3 — Pattern 7 applied (Simple/Complex)

**Epic:** "Flight search with max stops, nearby airports, flexible dates"

**Pattern 7 check:** "What's the simplest version?" → basic origin/destination/date search

**Split:**
1. Basic flight search (origin, destination, date) — **core value**
2. Add max stops filter — enhancement
3. Add nearby airports option — enhancement
4. Add flexible dates option — enhancement

**Split Evaluation:**
- ✅ Reveals low-value work: user research shows "flexible dates" is rarely used → candidate to kill or defer
- ✅ Equal-sized stories: story 1 = 3 days, others = 1 day each

### Example 4 — Iterative splitting (multiple patterns applied in sequence)

**Epic:** "Checkout flow with discounts (member, VIP, first-time) and payment (Visa, Mastercard, Amex)"

**First pass — Pattern 1 (Workflow):** YES
- Story 1: Add items to cart
- Story 2: Apply discount
- Story 3: Complete payment

**Check Story 2 ("Apply discount"):** still estimated at 4 days → too large, re-split

**Second pass on Story 2 — Pattern 3 (Business Rules):** YES
- Story 2a: Apply member discount (10%)
- Story 2b: Apply VIP discount (20%)
- Story 2c: Apply first-time discount (5%)

**Check Story 3 ("Complete payment"):** still estimated at 5 days → too large, re-split

**Third pass on Story 3 — Pattern 6 (Major Effort):** YES
- Story 3a: Accept Visa payments (build the full payment infrastructure)
- Story 3b: Add Mastercard, Amex support (trivial additions once Visa infrastructure exists)

**Final breakdown:** 6 stories total, all sized 1-2 days each — this is what "restart at Pattern 1 for any story still too large" looks like in practice, applied twice in the same epic.

---

**End of Examples file.** Return to `Product-Management-Assistant.md` for the operating instructions and full card definitions these examples illustrate.
