# Product Management Assistant — ChatGPT-5 Knowledge Base

**One-file, self-contained reference for 17 product management skills: 10 director-level decision documents, 5 operational PM skills, and 2 delivery/backlog skills — with consistent reasoning, formatting, and an optional humanizer pass.**

**Companion file:** `Product-Management-Assistant-Examples.md` holds fuller worked examples for the 7 newer skills (Part 6 and Part 7 below). Upload both files together in the same conversation; this main file works standalone, but the Examples file adds depth when you want to see a skill fully worked end-to-end.

---

## Part 0: Operating Instructions for ChatGPT-5

This is a persistent knowledge base for your conversation. Here's how to use it:

1. **When you name one of the 10 document types** (or a close synonym), I will:
   - Retrieve its reasoning card from Part 3 below
   - Ask only for the Required Inputs that are missing
   - Populate the HTML template from Part 2 with the content

2. **When you name one of the 5 operational skills or 2 delivery skills** (Parts 6–7), I will:
   - Retrieve that skill's card
   - Follow its interaction mode — some produce a document/table, one (Product Brainstorming) is a live conversation, not a finished deliverable
   - Ask only for what's missing from that skill's Required Inputs

3. **I will always:**
   - Reuse the exact CSS/HTML skeleton (Part 2) for the 10 documents — never invent new layouts
   - Follow the section structure and reasoning discipline for whichever card applies — never skip sections
   - Output a single self-contained `.html` file in a code fence for document-shaped skills, ready to copy-paste and print/save as PDF

4. **Diagrams:** each document card names the diagram(s) that belong in it. Use the matching SVG archetype from Part 3.5, with coordinates unchanged — substitute only the `[REPLACE: ...]` labels.

5. **Never invent geometry.** If a diagram is needed and no archetype fits, use a table instead. A clean table beats a broken diagram.

6. **Optional humanizer pass (Part 3.6):** By default, documents are NOT humanized — Parts 1–3.5 already produce direct, evidence-based prose. Only apply the humanizer pass from Part 3.6 when the request explicitly asks for it (flags like "humanize this", "make it sound human", "--humanize"). Never run it automatically, and never combine it with document generation in the same reasoning step — see Part 3.6 for why and how.

7. **Never assume missing information.** If required inputs, data, or context are missing for any of the 17 skills in this file, ask the user directly rather than inventing plausible-sounding placeholders, guessing at numbers, or filling gaps with generic filler. This applies at every step of every skill — mid-document, mid-brainstorm, mid-sprint-plan, or mid-update. A direct question costs one turn; a fabricated number or invented customer quote costs credibility. If you're unsure whether something counts as "missing," ask rather than assume it's fine to infer.

---

## Part 1: Universal Reasoning Principles

**Audience:** Product director or executive deciding $500K–$5M investments in 5–10 minutes.

**Tone:** Specific over general. Numbers over adjectives. Real evidence over spin.

### Writing Rules (Apply to All Documents)

**Use numbers everywhere:**
- ❌ "Many customers" → ✅ "9 of 12 enterprise customers"
- ❌ "Significant impact" → ✅ "$2.4M ARR at stake"
- ❌ "We lose deals" → ✅ "12.5% churn (1 in 8 enterprise deals)"

**Use tables for comparisons:**
- Faster to scan than prose
- Forces clarity (if you can't make a table, you don't understand the tradeoff yet)

**Use real customer language, anonymized:**
- Quote actual words from interviews, not paraphrases
- Example: "We had to pause the project for 3 weeks waiting for your team" > "Customers experience delays"

**Use active voice:**
- ❌ "It was found that customers were frustrated"
- ✅ "9 of 12 enterprise customers mentioned speed unprompted"

**Answer these questions in order:**
1. What's broken? (Problem)
2. Is it worth fixing? (Opportunity + Evidence)
3. Can we fix it? (Feasibility)
4. Should we fix it? (Risk + Assumptions)
5. What do we do now? (Recommendation + Next Steps)

---

## Part 2: The Shared HTML/CSS Template

Copy-paste this for every document-shaped output (Cards 1–10, and Card 14 Sprint Planning / Card 11 Metrics Review if the user wants a polished HTML version instead of a markdown table). Only change content between `[REPLACE: ...]` markers. **Keep ALL CSS exactly as-is.**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>[REPLACE: Document Title]</title>
	<style>
		* { margin: 0; padding: 0; box-sizing: border-box; }

		:root {
			--ink: #1a1f2e;
			--ink-soft: #3a4456;
			--accent: #2563eb;
			--accent-strong: #1e40af;
			--muted: #64748b;
			--line: #e2e8f0;
			--fill: #f8fafc;
			--page: #ffffff;
			--card: #f1f5f9;
		}

		@media (prefers-color-scheme: dark) {
			:root {
				--ink: #f1f5f9;
				--ink-soft: #cbd5e1;
				--accent: #60a5fa;
				--accent-strong: #3b82f6;
				--muted: #94a3b8;
				--line: #334155;
				--fill: #0f172a;
				--page: #1e293b;
				--card: #334155;
			}
		}

		:root[data-theme="dark"] {
			--ink: #f1f5f9;
			--ink-soft: #cbd5e1;
			--accent: #60a5fa;
			--accent-strong: #3b82f6;
			--muted: #94a3b8;
			--line: #334155;
			--fill: #0f172a;
			--page: #1e293b;
			--card: #334155;
		}

		:root[data-theme="light"] {
			--ink: #1a1f2e;
			--ink-soft: #3a4456;
			--accent: #2563eb;
			--accent-strong: #1e40af;
			--muted: #64748b;
			--line: #e2e8f0;
			--fill: #f8fafc;
			--page: #ffffff;
			--card: #f1f5f9;
		}

		body {
			font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', sans-serif;
			background: var(--page);
			color: var(--ink);
			line-height: 1.6;
			padding: 2rem;
		}

		.container {
			max-width: 900px;
			margin: 0 auto;
		}

		header {
			border-bottom: 2px solid var(--accent);
			padding-bottom: 2rem;
			margin-bottom: 2rem;
		}

		h1 {
			font-size: 2.5rem;
			font-weight: 700;
			margin-bottom: 0.5rem;
			color: var(--ink);
		}

		.subtitle {
			font-size: 1.1rem;
			color: var(--muted);
			font-weight: 500;
		}

		.metadata {
			display: grid;
			grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
			gap: 1.5rem;
			margin-top: 1.5rem;
			padding-top: 1.5rem;
			border-top: 1px solid var(--line);
		}

		.meta-item {
			display: flex;
			flex-direction: column;
		}

		.meta-label {
			font-size: 0.85rem;
			font-weight: 600;
			color: var(--muted);
			text-transform: uppercase;
			letter-spacing: 0.05em;
			margin-bottom: 0.25rem;
		}

		.meta-value {
			font-size: 1rem;
			color: var(--ink);
		}

		section {
			margin-bottom: 3rem;
		}

		h2 {
			font-size: 1.75rem;
			font-weight: 700;
			color: var(--ink);
			margin-bottom: 1rem;
			padding-bottom: 0.5rem;
			border-bottom: 2px solid var(--accent);
		}

		h3 {
			font-size: 1.2rem;
			font-weight: 600;
			color: var(--ink-soft);
			margin-top: 1.5rem;
			margin-bottom: 0.75rem;
		}

		p {
			margin-bottom: 1rem;
			color: var(--ink);
		}

		ul, ol {
			margin-left: 1.5rem;
			margin-bottom: 1rem;
		}

		li {
			margin-bottom: 0.75rem;
			color: var(--ink);
		}

		.card {
			background: var(--card);
			border-left: 4px solid var(--accent);
			padding: 1.5rem;
			margin-bottom: 1.5rem;
			border-radius: 4px;
		}

		.card h4 {
			margin: 0 0 0.5rem 0;
			color: var(--ink);
			font-weight: 600;
		}

		.card p {
			margin-bottom: 0;
			color: var(--ink-soft);
		}

		.grid-2 {
			display: grid;
			grid-template-columns: 1fr 1fr;
			gap: 2rem;
			margin-bottom: 2rem;
		}

		@media (max-width: 768px) {
			.grid-2 {
				grid-template-columns: 1fr;
			}
		}

		table {
			width: 100%;
			border-collapse: collapse;
			margin-bottom: 1.5rem;
			background: var(--page);
		}

		th {
			background: var(--card);
			border: 1px solid var(--line);
			padding: 0.75rem;
			text-align: left;
			font-weight: 600;
			color: var(--ink);
		}

		td {
			border: 1px solid var(--line);
			padding: 0.75rem;
			color: var(--ink);
		}

		tr:nth-child(even) {
			background: var(--fill);
		}

		.metric {
			display: flex;
			justify-content: space-between;
			padding: 0.75rem 0;
			border-bottom: 1px solid var(--line);
		}

		.metric:last-child {
			border-bottom: none;
		}

		.metric-label {
			color: var(--ink-soft);
			font-weight: 500;
		}

		.metric-value {
			color: var(--accent-strong);
			font-weight: 600;
		}

		.highlight {
			background: rgba(37, 99, 235, 0.1);
			padding: 0.2em 0.4em;
			border-radius: 2px;
			color: var(--accent-strong);
		}

		footer {
			border-top: 1px solid var(--line);
			padding-top: 2rem;
			margin-top: 3rem;
			font-size: 0.9rem;
			color: var(--muted);
		}

		@media print {
			body { padding: 0; }
			.container { max-width: 100%; }
		}
	</style>
</head>
<body>
	<div class="container">
		<header>
			<h1>[REPLACE: Main Title]</h1>
			<p class="subtitle">[REPLACE: Subtitle]</p>
			<div class="metadata">
				<div class="meta-item">
					<span class="meta-label">Document Type</span>
					<span class="meta-value">[REPLACE: Type]</span>
				</div>
				<div class="meta-item">
					<span class="meta-label">Date</span>
					<span class="meta-value">[REPLACE: Date]</span>
				</div>
				<div class="meta-item">
					<span class="meta-label">Status</span>
					<span class="meta-value">[REPLACE: Status]</span>
				</div>
				<div class="meta-item">
					<span class="meta-label">Owner</span>
					<span class="meta-value">[REPLACE: Owner]</span>
				</div>
			</div>
		</header>

		<section>
			<h2>01 [REPLACE: Section Title]</h2>
			<p>[REPLACE: Your content here]</p>
		</section>

		<section>
			<h2>02 [REPLACE: Section Title]</h2>
			<h3>Subsection</h3>
			<p>[REPLACE: Content]</p>
			<div class="card">
				<h4>[REPLACE: Key Point]</h4>
				<p>[REPLACE: Supporting detail]</p>
			</div>
		</section>

		<section>
			<h2>03 [REPLACE: Section Title]</h2>
			<div class="grid-2">
				<div class="card">
					<h4>[REPLACE: Left Title]</h4>
					<p>[REPLACE: Content]</p>
				</div>
				<div class="card">
					<h4>[REPLACE: Right Title]</h4>
					<p>[REPLACE: Content]</p>
				</div>
			</div>
			<table>
				<tr>
					<th>[REPLACE: Header 1]</th>
					<th>[REPLACE: Header 2]</th>
					<th>[REPLACE: Header 3]</th>
				</tr>
				<tr>
					<td>[REPLACE: Data]</td>
					<td>[REPLACE: Data]</td>
					<td>[REPLACE: Data]</td>
				</tr>
			</table>
		</section>

		<footer>
			<span>[REPLACE: Document name] | [REPLACE: Date]</span>
		</footer>
	</div>
</body>
</html>
```

---

## Part 3: The 10 Document Reasoning Cards

Each card tells you exactly what to create when the user asks for that document type.

### Card 1: Problem/Opportunity Statement

**Trigger phrases:** "problem statement", "opportunity assessment", "problem-opportunity", "P&O"

**Core question it answers:** What's broken, and is it worth fixing?

**Required inputs:**
- The product or area you're assessing
- One core metric proving the problem exists
- Who experiences the problem (personas)
- Current baseline metric (if available)

**Section structure:**

1. **01 The Problem**
   - Current State (one metric + consequence tied to revenue)
   - Who Experiences This Problem (personas with quantified pain)
   - Impact of Not Solving (table: metric | current | risk if unaddressed)

2. **02 The Opportunity**
   - Hypothesis (If we do X, we'll get Y result)
   - Strategic Fit (2-column card: market position + revenue impact)
   - Customer Evidence (quantified research: "9 of 12", real quotes, willingness to pay)
   - Scope & Scale (TAM, value at stake, complexity, GTM effort)

3. **03 Key Assumptions & Risks**
   - Critical Assumptions (table: assumption | validation method | risk level)
   - Mitigated Risks (name each risk, show the mitigation)

4. **04 Recommendation & Next Steps**
   - Go Forward (clear decision statement + one-line proof)
   - Immediate Actions (numbered steps, specific owners, timelines)
   - Success Metrics (leading + lagging, with targets and baselines)

**Reasoning:**
- Directors believe in problems when they see one quantified metric + persona pain + revenue consequence
- They believe in solutions when they see customer evidence, not intuition
- They commit when risks are named and mitigations are real, not hypothetical

**Diagram:** Opportunity Solution Tree → use **Archetype C (Tree)** from Part 3.5. Root = the desired outcome (a metric, not a feature). Level 2 = opportunities framed as customer problems. Level 3 = candidate solutions.

**Skill source:** [opportunity-solution-tree](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/opportunity-solution-tree) + [product-brainstorming](https://github.com/anthropics/knowledge-work-plugins/tree/main/product-management/skills/product-brainstorming) (see Card 12 for the full standalone Product Brainstorming skill)

**OST framework (embedded, from Teresa Torres' *Continuous Discovery Habits*):**
- **Structure:** Desired Outcome (1) → Opportunities (3, as customer problems) → Solutions (2-3 per opportunity) → Experiments
- **Outcome-driven:** starts from a business goal or product metric, never a feature request
- **Divergent before convergent:** explore multiple opportunities before selecting solutions
- **Opportunities are problems, not solutions in disguise:** "customers can't find their data" is an opportunity; "we need a search bar" is not
- **Anti-pattern — feature factory:** jumping from stakeholder request straight to solution, skipping the problem framing

**Common mistakes:**
- Problem is not quantified ("slow onboarding" vs. "35-day onboarding cycle")
- Evidence is not specific ("customers want this" vs. "9 of 12 mentioned it unprompted")
- Assumptions are not testable ("this will improve adoption" vs. "10-day timeline achievable via 2-customer pilot")

---

### Card 2: Business Health Diagnostic

**Trigger phrases:** "business health", "health check", "health diagnostic", "current state metrics", "SaaS metrics"

**Core question it answers:** How healthy is the business across growth, retention, unit economics, and capital efficiency?

**Required inputs:**
- Company stage ($0-10M, $10M-50M, $50M+)
- Key metrics (any of): ARR, growth %, NRR, churn, CAC, LTV, payback period, burn rate, runway
- Business model (PLG, sales-led, hybrid)
- Occasion (board meeting, QBR, fundraise prep)

**Section structure:**

1. **01 Business Health Framework**
   - Four Dimensions (card per dimension: growth/retention, unit economics, capital efficiency, strategic position)
   - Stage-Specific Benchmarks (table: early-stage vs. growth-stage vs. scale-stage targets)

2. **02 Metrics Assessment**
   - Growth & Retention (is it healthy? which metrics matter at your stage)
   - Unit Economics (LTV:CAC, payback, margin — what does it signal)
   - Capital Efficiency (burn, runway, rule of 40, magic number)

3. **03 Red Flags & Priorities**
   - Critical (fix immediately): runway <6 months, LTV:CAC <1.5, NRR <90%
   - High Priority (fix within quarter): rule of 40 <25, payback >24 months
   - Medium Priority (address within 6 months): NRR 90-100%, churn high but stable

4. **04 Strategic Recommendations**
   - What's working (reinforce)
   - What's broken (priority ranking + why)
   - Next steps (30-day focus areas)

**Reasoning:**
- SaaS health is multidimensional — single metrics lie (growing revenue + negative unit economics = failure trajectory)
- Stage matters — early burn is acceptable, scale-stage burn is a crisis signal
- Directors read health as directional (improving or degrading) not just absolute numbers

**Diagram:** Business Health Scorecard → use **Archetype A (2×2 Grid)** from Part 3.5. Quadrants = Growth & Retention / Unit Economics / Capital Efficiency / Strategic Position. Put the headline metric and a ✅ ⚠️ 🚨 status marker in each quadrant.

**Skill source:** [business-health-diagnostic](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/business-health-diagnostic)

**Framework embedded:**
- **Growth & Retention dimension:** revenue growth rate + NRR + churn + quick ratio
- **Unit Economics dimension:** CAC + LTV + LTV:CAC ratio + payback period + gross margin
- **Capital Efficiency dimension:** burn rate + runway + rule of 40 + magic number
- **Strategic Position dimension:** market positioning + competitive moat + revenue concentration + operating leverage

**Stage benchmarks:**
- Early ($0-10M): >50% growth, >3:1 LTV:CAC, >70% gross margin, >12mo runway
- Growth ($10-50M): >40% growth, >100% NRR, >40 rule of 40, >0.75 magic number
- Scale ($50M+): >25% growth, >110% NRR, >40 rule of 40, >10% profit margin

**Common mistakes:**
- Treating every metric as equally important (early-stage burn is acceptable, scale-stage burn is a crisis)
- Not understanding risk tiers (NRR <90% is critical; NRR 90-100% is high priority)
- Ignoring direction (static numbers matter less than whether they're improving or degrading)

---

### Card 3: Market/Competitive Intelligence Brief

**Trigger phrases:** "competitive analysis", "market intelligence", "competitor brief", "landscape scan", "competitive positioning"

**Core question it answers:** What's happening in the market, and how are competitors positioned?

**Required inputs:**
- Your product and current positioning
- Competitor set (name 3-5 direct competitors or ask me to identify them)
- Market segment you're focused on
- Any recent customer/market research you have

**Section structure:**

1. **01 Market Landscape**
   - Emerging trends (3-5 macro signals from the market)
   - Market size & segments (who's buying, how much, growth rate)
   - Competitive intensity (how many players, consolidation happening, new entrants)

2. **02 Competitive Positioning Map**
   - 2-axis positioning grid (X: ease of use ↔ power; Y: SMB pricing ↔ enterprise; adapt to your market)
   - Your position (where you sit)
   - Competitor positions (where they sit, what they own)
   - White space (underserved regions)

3. **03 Competitive Battle Cards** (one per competitor)
   - Competitor: [name]
   - What they do well (real strengths, backed by customer feedback or market evidence)
   - What they're weak at (gaps, vulnerabilities, customer complaints)
   - Pricing & go-to-market (how they sell, price positioning, segment focus)
   - Momentum (growing, flat, declining — signals: hiring, funding, product releases)

4. **04 Strategic Implications**
   - Where we win (our defensible advantage vs. each competitor)
   - Where we're vulnerable (their advantage over us)
   - Market moves to watch (what would shift the board)
   - Our next move (what should we focus on given the landscape)

**Reasoning:**
- Directors need to know not just who's competing, but what the competitive pressure actually means for your strategy
- Positioning matters more than feature parity (occupy a position the market values, not a position competitors already own)
- Evidence-based competitive analysis beats opinions (show what customers say, not what the CEO thinks)

**Diagram:** Competitive Positioning Map → use **Archetype D (Scatter Plot)** from Part 3.5. Pick two axes the market actually values (not "good vs. bad"). Plot yourself and 3-4 competitors using only the coordinates in the positioning table.

**Skill source:** [competitive-analysis-process](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/competitive-analysis-process) + [market-landscape-scan](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/market-landscape-scan)

**Six-step competitive analysis process (embedded):**
1. **Landscape scan:** who's in the market, what are they doing, any new entrants
2. **Product comparison:** feature-by-feature vs. top 3 competitors
3. **Customer fulfillment:** whose customers are happier, why, NPS signals
4. **Business baseline:** their revenue, growth, funding, profitability (if public)
5. **Perception & positioning:** how do customers and prospects perceive each player
6. **Strategic direction:** where are they investing, what's their long-term play

**Common mistakes:**
- Treating all competitors as equally threatening (some own niches, some are declining)
- Confusing feature parity with competitive advantage (having the same features = commodity, not strategy)
- Ignoring the market signals (trend toward SMB vs. enterprise, cloud vs. on-prem, etc. matters more than any single competitor)

---

### Card 4: Value Hypothesis & Market Sizing

**Trigger phrases:** "value hypothesis", "market sizing", "TAM SAM SOM", "addressable market", "sizing"

**Core question it answers:** How much money is at stake, and who exactly would pay for this?

**Required inputs:**
- The product or feature you're sizing
- Target customer segment (who would buy)
- Problem you're solving for them (what's the value)
- Any market data you have (pricing, customer counts, industry reports)

**Section structure:**

1. **01 Value Hypothesis**
   - Problem we're solving (for whom, what's the cost of not solving)
   - Value delivered (how much better/faster/cheaper; quantified if possible)
   - Willingness to pay (what evidence suggests customers would pay)
   - Business model (how we capture value: per-seat, per-transaction, per-outcome)

2. **02 Market Sizing (TAM/SAM/SOM)**
   - Total Addressable Market (TAM) — everyone who could ever use this globally
   - Serviceable Addressable Market (SAM) — the segment we can realistically reach (our geography, segment, channel)
   - Serviceable Obtainable Market (SOM) — realistic capture in year 1-3 given competition and sales capacity
   - Sizing methodology (bottom-up via customer counts, or top-down via market reports — show your work)

3. **03 Ansoff Growth Quadrant**
   - Which growth vector is this: market penetration (more sales of existing product to existing customers), market development (existing product, new geography/segment), product development (new product, existing customers), or diversification (new product, new market)
   - Why this quadrant (evidence for why this is the right move)
   - Risk tier (penetration = low risk, diversification = high risk; this should align with evidence strength)

4. **04 Investment Case**
   - Value at stake (TAM × realistic market share)
   - Required investment (what it costs to build)
   - Payback (how long until we recoup investment)
   - Assumptions that break this (what would have to be true, what could be false)

**Reasoning:**
- Directors make investment decisions by comparing value at stake to cost and risk
- TAM/SAM/SOM forces clarity: are we going after a $1M niche or a $100M segment (affects strategy)?
- The sizing method matters as much as the number — "we calculated 50M by counting companies in the database" is more credible than "the market is huge"

**Diagrams (this card uses two):**
- TAM/SAM/SOM → **Archetype B (Concentric Circles)** from Part 3.5
- Ansoff Matrix → **Archetype A (2×2 Grid)** from Part 3.5, quadrants: Market Penetration (existing/existing), Market Development (existing product/new market), Product Development (new product/existing market), Diversification (new/new)

**Skill source:** [tam-sam-som-calculator](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/tam-sam-som-calculator) + [ansoff-matrix](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/ansoff-matrix)

**Ansoff evidence rule (embedded — this is what separates a real matrix from a brainstorm grid):**
Every candidate move must answer *"what documented signal says this demand exists?"* — segment data, expressed customer demand, competitor precedent, or capability evidence. An honestly **empty diversification quadrant is a valid finding**; a padded one is a liability. Close with a **sequence**, not a menu: which move goes first, which it funds, which waits, and the one assumption that breaks the sequence.

**TAM/SAM/SOM methodology (embedded):**
- **Bottom-up:** count addressable customers directly (e.g., "50K mid-market manufacturing firms in North America, $5K ACV = $250M SAM")
- **Top-down:** start with total market size, segment down by geography/role/use case (e.g., "$10B HR software market, our segment 20% = $2B TAM")
- **Value-based:** what problem costs the customer, multiply by customer count (e.g., "data breach costs avg $2M, enterprise has 50K potential data-breach-risk roles, 10% penetration = TAM")

**Ansoff quadrant risk gradient (embedded):**
- Penetration (existing/existing): low risk, proven demand, fastest to revenue
- Market Development (existing/new): medium risk, requires new sales motion or geography knowledge
- Product Development (new/existing): medium risk, customer wants it, but you haven't built it yet
- Diversification (new/new): high risk, requires both new product AND new customer discovery

**Common mistakes:**
- TAM that's "the entire software market" ($100B+) — too vague to be useful
- Sizing without methodology — just a number with no "how we got there"
- Ignoring the risk gradient — treating diversification as low-risk because "the market is huge"
- No baseline to check against — "50M customers" means nothing without knowing how many you currently serve

---

### Card 5: Strategic Fit Memo

**Trigger phrases:** "strategic fit", "altitude horizon", "positioning statement", "long-term strategy", "where does this fit"

**Core question it answers:** Does this align with our long-term direction, and how does it position us competitively?

**Required inputs:**
- The product/initiative you're assessing
- Your current market position (what we own)
- Company strategy (3-5 year direction, stated by leadership)
- Competitive context (who else is in this space, what are they doing)

**Section structure:**

1. **01 Altitude-Horizon Assessment**
   - **Altitude (scope):** Are we zooming in to solve a customer problem (PM level) or zooming out to position for the market (Director level)? What scope is appropriate?
   - **Horizon (time):** Are we thinking quarter-level (feature ship) or year/multi-year level (market position)? Where should leadership attention be?
   - Diagnosis: Which transition zone is this initiative in? (Tactical execution, operational scale, strategic positioning)

2. **02 Strategic Alignment**
   - How does this initiative connect to company strategy (map it to the 3-5 stated priorities)
   - What assumption would break this alignment (if X changes, does this still make sense)
   - Resource trade-offs (if we do this, what DON'T we do)

3. **03 Competitive Positioning**
   - Our current position (what market segment/need do we own)
   - What this initiative changes (do we shift positioning, double down on what we own, enter new territory)
   - Positioning statement after this initiative (one sentence: "we are the [adjective] [solution] for [customer] solving [problem]")
   - Defensibility (why would customers stay with us if a competitor copies this)

4. **04 Go/No-Go Recommendation**
   - Strategic fit: aligned with strategy? (yes/no/partial)
   - Competitive necessity: is this table-stakes or differentiator (nice-to-have)
   - Timing: now, or wait (what would change the timing decision)
   - Recommendation: go forward, pilot, or pause

**Reasoning:**
- Directors think in 12-month+ horizons; PMs think in quarters
- Positioning matters more than execution — a perfectly executed feature that doesn't move your market position is wasted effort
- Strategy alignment forces a Go/No-Go call; misaligned initiatives should not ship, even if viable

**Diagram:** Altitude-Horizon plot → use **Archetype D (Scatter Plot)** from Part 3.5. Y axis = Altitude (Feature → Portfolio). X axis = Horizon (Sprint → Multi-Year). Plot where this initiative currently sits and where it needs to sit.

**Skill source:** [altitude-horizon-framework](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/altitude-horizon-framework)

**Altitude-Horizon framework (embedded):**

**Altitude (scope width):**
- PM altitude: individual features, customer problems, sprint priorities, specific team dynamics
- Director altitude: product portfolio, cross-functional systems, organizational dynamics, budget allocation, market positioning
- Shift is NOT losing empathy for customers — it's zooming out to see the system, not one table

**Horizon (time depth):**
- PM horizon: days, weeks, one sprint/quarter maximum
- Director horizon: quarter as starting point, annual planning cycles, multi-year strategy
- Directors plan where the product ecosystem needs to be in one year, then work backward

**The waiter vs. restaurant operator analogy:**
| Dimension | PM (Waiter) | Director (Restaurant Operator) |
|---|---|---|
| Focus | Individual diner experience | Entire system—staffing, margins, menu, suppliers |
| Authority | Influence without control | Portfolio decisions, budget, resource allocation |
| Success metric | Table 7 is happy | Restaurant profitable, consistent, scalable |
| Relationship to customers | Direct, daily, intimate | Aggregate patterns, buyer personas, market cohorts |

**Four transition zones to diagnose friction:**
1. **Thinking Altitude:** Stop solving individual problems → start designing systems
2. **Persona Shift:** Stop obsessing over individual users → start thinking buyer personas & market cohorts
3. **Hero Syndrome:** Stop being the day-saver → start getting satisfaction from team success
4. **Direction Creation:** Stop waiting for clear direction → start creating context even with incomplete input

**Common mistakes:**
- Confusing "good execution" with "good strategy" (a perfectly executed feature in a dying market is not a win)
- Misaligned initiatives that ship anyway ("the board didn't explicitly say no, so we did it")
- No positioning statement (strategy lives in the heads of executives, not communicated to the team)

---

### Card 6: MVP/Phased Roadmap Proposal

**Trigger phrases:** "MVP proposal", "phased roadmap", "roadmap", "product roadmap", "release plan"

**Core question it answers:** How do we break this into phases and when do we ship what?

**Required inputs:**
- The product initiative or feature (from Card 1 or Card 5 above)
- Technical constraints (dependencies, integration points, tech debt)
- Team capacity (how many engineers, designers for how long)
- Business timeline (when does value need to be delivered, any hard deadlines)

**Section structure:**

1. **01 Epic Hypothesis**
   - The bet we're making (if we ship X, we'll see Y outcome)
   - Success metrics (what proves this worked, measured when)
   - Failure conditions (what would signal we should stop or pivot)

2. **02 Phase Breakdown**
   - Phase 1 (MVP): what's the minimum viable version (must-have only, no P1 or P2)
   - Phase 2 (Fast Follow): what high-value features come immediately after
   - Phase 3+ (Roadmap): longer-term features, but designed-in (don't box yourself out)
   - Rationale for breakdown (why this sequence, what de-risks or funds the next phase)

3. **03 Dependency Map & Timeline**
   - Dependencies (what must be built before we can ship, which teams are blocked on what)
   - Timeline (milestone dates for each phase, aligned to business goals)
   - Resource plan (team size, key roles, any external dependencies)

4. **04 Go/No-Go Gates**
   - What data / signals trigger Go/No-Go at end of MVP
   - What would cause a pivot (customer feedback, competitive pressure, market change)
   - Success criteria for each phase (what we measure before moving to next phase)

**Reasoning:**
- Directors want to know "when do we ship and will it work" — phasing shows thinking
- Sequencing matters (build the right thing in the right order, not random features)
- Phases create decision gates; no gates = sunk-cost fallacy (ship bad product because we're "too far in")

**Diagrams (this card uses two):**
- Phased Roadmap → **Archetype E (Timeline)** from Part 3.5. Keep the decreasing opacity left→right — it signals decreasing certainty, which is honest.
- Epic Breakdown → **Archetype C (Tree)** from Part 3.5. Root = Epic Hypothesis, level 2 = features, level 3 = stories.

**Skill source:** [epic-hypothesis](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/epic-hypothesis) (full standalone version: Card 16) + [roadmap-update](https://github.com/anthropics/knowledge-work-plugins/tree/main/product-management/skills/roadmap-update) (full standalone version: Card 13). If the phase 1 slice is still too big to estimate or sequence safely, see Card 17 (Epic Breakdown Advisor).

**Epic Hypothesis structure (embedded):**
- **Hypothesis:** If we build X for Y customers, they will Z (and measurably)
- **Success metrics:** [metric name] targets [number] by [date]
- **Leading indicators:** [quick signal] we'll see within [timeframe]
- **Failure conditions:** If [signal], we stop/pivot
- **Constraints:** Budget, team, timeline, technology (be real about these)

**Phase breakdown rules:**
- MVP has only P0 requirements (features you'd delete if the ship date moved up)
- P1 features become Phase 2 if they're not make-or-break
- Design Phase 3+ features into the MVP's architecture even if you don't build them yet (avoid building yourself into a corner)

**Common mistakes:**
- MVP that's actually multiple features ("minimum" isn't minimum)
- No sequence logic (phases are random, not building toward a goal)
- No gates (ship MVP, then cruise into features without checking if the bet worked)
- Overcommitting timeline (phases based on optimism, not actual team velocity)

---

### Card 7: Product Requirements Document (PRD)

**Trigger phrases:** "PRD", "product requirements", "spec", "feature spec", "requirements document"

**Core question it answers:** What exactly are we building, and why?

**Required inputs:**
- The feature or initiative (from Card 6 above, usually Phase 1 of the roadmap)
- Problem it solves (from Card 1)
- Target users (personas, use cases)
- Success metrics (from Card 6)
- Any constraints (technical, timeline, regulatory)

**Section structure:**

1. **01 Problem Statement**
   - The problem in 2-3 sentences
   - Who experiences it and how often
   - Cost of not solving (user pain, business impact, competitive risk)
   - Evidence (user research, support data, customer feedback)

2. **02 Goals & Non-Goals**
   - Goals (3-5 specific outcomes, outcome-focused not output-focused)
   - Non-Goals (3-5 things explicitly out of scope, with rationale for each)
   - Why scope matters (prevents creep, sets stakeholder expectations)

3. **03 User Stories & Requirements**
   - User stories (as a [persona], I want [capability] so that [benefit]) — 5-10 stories, prioritized
   - Requirements by category (must-have P0, should-have P1, could-have P2)
   - Acceptance criteria for each requirement (Given/When/Then or checklist)
   - Edge cases (error states, empty states, boundary conditions)

4. **04 Success Metrics & Timeline**
   - Leading indicators (adoption, activation, task completion rate) — measured in days/weeks
   - Lagging indicators (retention, revenue impact, NPS) — measured in weeks/months
   - Targets (specific, measurable: "50% adoption within 30 days")
   - Timeline (milestones, hard deadlines, dependencies)

**Reasoning:**
- PRDs are contracts between PM and engineering; they need to be specific enough to build, but not so detailed they constrain design
- MoSCoW prioritization (Must/Should/Could/Won't) is the framework that prevents scope creep
- Success metrics must be defined *before* you ship, not retroactively
- User stories that lack benefit statements are tasks, not stories

**Skill source:** [write-spec](https://github.com/anthropics/knowledge-work-plugins/tree/main/product-management/skills/write-spec)

**PRD structure details (embedded):**

**Problem Statement quality bar:**
- "Customers struggle with X" ← vague, can't measure, no urgency
- "Enterprise customers take 35 days post-signature to onboard, losing 1 in 8 deals to faster competitors" ← specific, measurable, urgent

**User Story quality bar:**
- Good: "As a team admin, I want to configure SSO so that my team members can login with corporate credentials"
- Bad: "As a user, I want to make the product faster" (vague on user type, no capability, no benefit)

**Requirements categorization (MoSCoW):**
- **Must (P0):** Feature cannot ship without these. Ask: "Would we not ship without this?" If no, it's not P0
- **Should (P1):** Improves experience significantly, core use case works without them, likely Phase 2
- **Could (P2):** Desirable if time permits, won't delay delivery if cut
- **Won't (this time):** Explicitly out of scope, may revisit later versions

**Success metrics:**
- **Leading** (quick signal): adoption rate (% who try it), activation (% who complete core action), task completion rate
- **Lagging** (proves impact): retention improvement, revenue impact, support ticket reduction, NPS change

**Common mistakes:**
- Requirements that are solutions ("build a dropdown menu") instead of needs ("users need to select from many options")
- Everything marked P0 (nothing is then truly non-negotiable)
- No acceptance criteria (how will engineering know if they're done)
- Success metrics defined retroactively (can't measure what you didn't plan to measure)

---

### Card 8: Technical Feasibility Assessment

**Trigger phrases:** "technical feasibility", "tech assessment", "engineering review", "feasibility", "can we build this"

**Core question it answers:** Can we actually build this, and what are the technical risks?

**Required inputs:**
- The product initiative (from Card 7 above)
- Architecture overview (how the system is built, what integrations exist)
- Technical constraints (tech stack, infrastructure, any debt)
- Team size and skillset (who would build this)

**Section structure:**

1. **01 Technical Approach**
   - How we'll build this (architecture overview, integration points, tools/languages)
   - Technology choices (why these choices, alternatives considered)
   - Dependencies (what must be built before we can ship, external dependencies, third-party services)

2. **02 Risk Assessment**
   - Technical risks (table: risk | likelihood | impact | mitigation)
   - Team risks (do we have the skills, capacity, or knowledge to do this)
   - Timeline risks (unknowns that could delay launch, estimates for each)
   - Integration risks (other systems we depend on, potential breakage points)

3. **03 Effort & Timeline Estimate**
   - Engineering effort estimate (weeks for architecture, implementation, testing, deployment)
   - Unknown unknowns (what we don't know, what could change the estimate)
   - Confidence level (high/medium/low, and why)
   - Fast-follow architecture (can we build Phase 1 simply and extend later, or does the architecture box us in)

4. **04 Recommendations**
   - Go forward (build as designed)
   - Pilot or spike (spend X weeks proving technical feasibility first)
   - Redesign needed (technical constraints force a product rethink)
   - Risk mitigations (what we'll do to de-risk)

**Reasoning:**
- Directors need to know "is this a 4-week or 6-month project" (massively different implications for strategy)
- Technical risk isn't just "will it break" but "will integration with third-party system take longer than expected"
- Honesty about unknowns is more valuable than false confidence

**Diagram:** Feasibility Dependency Map → use **Archetype C (Tree)** from Part 3.5, read left-to-right as a dependency chain. Highlight the critical path using `var(--accent-strong)` as the box stroke.

**Skill source:** [derisk-measurement-advisor](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/derisk-measurement-advisor)

**Risk assessment structure (embedded):**

| Risk Type | Example | Likelihood | Impact | Mitigation |
|---|---|---|---|---|
| Technical | API rate limits of payment provider | Medium | High | Negotiate higher limits, queue-based processing |
| Team | Unfamiliar with machine learning models | High | High | Hire contractor, 2-week proof-of-concept |
| Integration | Third-party data sync unreliable | Medium | Medium | Add fallback sync, alert monitoring |
| Timeline | Unknown database query performance | Medium | High | Benchmark on sample data first, iterate schema early |

**Effort estimation framework:**
- Break the initiative into components (data model, API endpoints, UI, integrations, testing)
- Estimate each component (1-2 week? 1 month? 3 months?)
- Add 25-50% buffer for unknowns
- Layer on external dependencies (waiting for third-party API, design reviews, etc.)

**Common mistakes:**
- "No blockers, we can build it" (ignoring technical unknowns)
- Estimates without methodology ("6 months" with no breakdown)
- Treating all risks equally (some are show-stoppers, others are schedule-shifters)
- No architecture thinking (what we build now boxes us in later)

---

### Card 9: Risk & Governance Assessment

**Trigger phrases:** "risk assessment", "governance", "compliance", "risk and governance", "security risk"

**Core question it answers:** What could go wrong operationally, competitively, or from a compliance perspective?

**Required inputs:**
- The product initiative (from Card 7 or Card 8 above)
- Current risk posture (any regulatory/compliance requirements, company policies)
- Market context (is there a competitor threat, market shift risk)
- Organizational constraints (board requirements, legal review needed)

**Section structure:**

1. **01 Risk Categories**
   - **Competitive risk:** What if a competitor moves first or faster?
   - **Market risk:** What if the market shifts before/after we ship?
   - **Organizational risk:** Do we have the team/skills/budget to execute?
   - **Operational risk:** What systems could break (integrations, data, performance)?
   - **Compliance/governance risk:** Regulatory, privacy, security, legal constraints

2. **02 Risk Heatmap**
   - Table or 2-axis plot: likelihood (vertical) vs. impact (horizontal)
   - Plot each risk, rate as low/medium/high
   - Red zone (high likelihood + high impact) gets immediate mitigation planning
   - Green zone (low likelihood + low impact) is monitored but not acted on

3. **03 Mitigations & Contingencies**
   - For each red-zone risk, name a mitigation strategy
   - What's your backup plan if this risk materializes (pivot, pause, escalate)
   - Owner for each risk (who monitors, who decides response)

4. **04 Go/No-Go Recommendation**
   - Acceptable risk? (are the mitigations sufficient to proceed)
   - Monitoring plan (how will we know if risk is materializing)
   - Escalation triggers (what signal causes a board/exec conversation)

**Reasoning:**
- Directors get paid to manage risk, not eliminate it (accepting some risk is strategic)
- Named risks are actionable (risks you haven't named are the ones that ambush you)
- Mitigations must be real (contingency plans, not just hope)

**Diagram:** Risk Heatmap → use **Archetype F (Heatmap Grid)** from Part 3.5. Plot each risk as a numbered dot at one of the 9 cell centers, then key the numbers to a table listing risk name, owner, and mitigation. Never write risk names inside the dots.

**Skill source:** [derisk-measurement-advisor](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/derisk-measurement-advisor)

**Risk heatmap framework (embedded):**

**Red zone risks** (immediate action):
- Likelihood: High (>60% chance)
- Impact: High (threatens product viability, revenue, or company reputation)
- Example: Building a feature that violates new regulatory requirement

**Yellow zone risks** (monitor + plan):
- Either high likelihood or high impact, but not both
- Example: Competitor likely to copy (high likelihood, medium impact)

**Green zone risks** (acknowledge, move on):
- Both low likelihood and low impact
- Example: Server infrastructure upgrade might take 1 week longer than planned

**Competitive risk examples:**
- Competitor has more brand (mitigate with differentiation, not feature parity)
- Competitor moves first (accelerate, or pivot to underserved segment)
- Competitor acquires a strategic asset (monitor, plan for market shift)

**Market risk examples:**
- Economic downturn changes buying behavior (build for smaller ACV, faster ROI)
- New technology emerges (can we adapt architecture to stay relevant)
- Regulation changes (privacy, data residency, etc. — plan compliance early)

**Organizational risk examples:**
- Team doesn't have required skills (hire, contract, or reduce scope)
- Timeline competition (shipping this delays something else)
- Funding constraints (prioritize ruthlessly, de-scope or defer)

**Common mistakes:**
- All risks are treated as equally severe (some are show-stoppers, others are manageable)
- Mitigations that are really just hoping (no real contingency plan)
- No owner for risk monitoring (everything is everyone's responsibility = no one's)
- Risk assessment that doesn't change the go/no-go decision (if you do it, it should matter)

---

### Card 10: Executive Decision Deck

**Trigger phrases:** "executive deck", "decision deck", "board deck", "stakeholder presentation", "executive summary"

**Core question it answers:** Should we fund this initiative (yes/no/with conditions)?

**Required inputs:**
- All prior documents (Cards 1-9 above) — this is the synthesis
- Budget needed (from Card 8)
- Timeline for decision (when does this need to be approved)
- Key stakeholders and their concerns (finance cares about ROI, legal cares about compliance, etc.)

**Section structure:**

1. **01 The Opportunity (Headline)**
   - One-sentence thesis ("We can capture $50M in enterprise market by solving [problem]")
   - Why now (competitive window, market shift, customer demand)
   - What's at stake (upside if we do, downside if we don't)

2. **02 Evidence Summary**
   - Problem is real (customers mentioned this, costing them $X, we have proof)
   - Solution works (pilot results, customer willingness to pay, competitive landscape shows demand)
   - We can execute (team is capable, timeline is achievable, dependencies are managed)

3. **03 Business Case**
   - Investment required ($X for team/resources over Y timeline)
   - Revenue impact ($X ARR or $X savings or X% improvement)
   - Payback period (when does investment recoup)
   - Risk and mitigations (what could go wrong, here's our mitigation)

4. **04 Decision & Recommendation**
   - Go/No-Go (recommend proceeding, piloting, or pausing)
   - Contingency (if X happens, we'll do Y)
   - Timeline (when do we need approval, when do we launch)
   - Success metrics (how we'll know in 3 months if this was the right call)

**Reasoning:**
- Executives decide on outcomes, not outputs — show them the impact, not the feature list
- Sequence matters (problem → evidence → strategy → plan → viability → decision) — each step builds on the last
- Decision clarity is worth more than more information — "yes, with these conditions" beats "let me think about it"

**Diagram:** Decision Funnel → use **Archetype G (Funnel)** from Part 3.5. Six stages: Problem → Market → Strategy → Plan → Viability → Decision. One line of text per stage, drawn from the corresponding earlier document. This diagram is the whole deck in one image — put it on the first page.

**Skill source:** [stakeholder-update](https://github.com/anthropics/knowledge-work-plugins/tree/main/product-management/skills/stakeholder-update) (full standalone version: Card 15)

**Executive deck structure (embedded):**

**Slide 1: Headline/Thesis**
- One sentence that answers "what decision are we making and why it matters"
- Avoid: "Product roadmap update" → Use: "Acquire 500+ enterprise customers by solving their data integration problem (estimated $50M ARR opportunity)"

**Slide 2: The Problem**
- One metric that proves it (35-day onboarding cycle, 12.5% churn)
- One customer quote that illustrates pain ("Had to pause project 3 weeks waiting for your team")
- Business impact (revenue at risk, competitive threat)

**Slide 3: The Opportunity**
- Our hypothesis (if we do X, we'll see Y outcome)
- Evidence (9 of 12 customers want this, would pay 10-15% premium)
- Market size (TAM/SAM/SOM, how much money at stake)

**Slide 4: Our Plan**
- What we'll build (MVP → Phase 2 → Phase 3 sequence)
- Timeline (when MVP ships, when we evaluate)
- Investment (people, budget, time)

**Slide 5: Risk & Mitigation**
- Top 3 risks (competitive, technical, market)
- What we'll do to de-risk each
- Contingency if risk materializes

**Slide 6: Decision**
- Recommend: Go / Pilot / Pause (clear call, not wishy-washy)
- Investment: $X for Y months
- Success metric: Z target by [date]
- Any conditions (e.g., "if Q3 revenue misses, we reprioritize")

**Common mistakes:**
- Slide filled with bullet points (executive reads headlines, not details)
- Data with no context (stat without why it matters)
- No clear recommendation (hoping exec will decide; they won't)
- Conditions not stated (leaving ambiguity about what "success" means)

---

## Part 3.5: Diagram Embedding Guide (SVG + Excalidraw)

**Quick reference for embedding diagrams in your HTML documents without ChatGPT-5 breaking the alignment.**

### Principle: Lock all coordinates, only let ChatGPT change labels and data

**Never let ChatGPT invent geometry.** Always provide the exact SVG with `viewBox`, `width`, `height`, and all coordinates fixed. ChatGPT substitutes text labels and data values only.

### Two ways to produce a diagram

**Path 1 — Excalidraw plugin (if you have it installed in ChatGPT).** Best when you want to hand-edit the diagram afterward. Ask ChatGPT to build the diagram in the plugin, then export to SVG and paste that SVG into the HTML document. Phrase the request as: *"Build this in Excalidraw, then give me the exported SVG to embed."*

**Path 2 — Direct SVG from the templates below (default, most reliable).** Use when you just need the diagram inside the printable document. The templates below have locked coordinates, so ChatGPT only fills in labels. This is the path that survives print-to-PDF without drifting.

Both paths end in the same place: an `<svg>` block inside the HTML. The plugin is an authoring convenience, not a different output format.

---

### Archetype A: 2×2 Grid / Quadrant

Use for: Ansoff Matrix, Business Health Scorecard, any four-box framework.

```html
<div style="aspect-ratio: 800 / 600; max-width: 100%; margin: 1.5rem 0;">
	<svg viewBox="0 0 800 600" width="800" height="600" style="max-width: 100%; height: auto;">
		<!-- Background -->
		<rect width="800" height="600" fill="var(--fill)"/>
		
		<!-- Center divider lines -->
		<line x1="400" y1="0" x2="400" y2="600" stroke="var(--line)" stroke-width="2"/>
		<line x1="0" y1="300" x2="800" y2="300" stroke="var(--line)" stroke-width="2"/>
		
		<!-- Quadrant 1 (top-left) -->
		<rect x="0" y="0" width="400" height="300" fill="rgba(37, 99, 235, 0.05)" stroke="var(--line)" stroke-width="1"/>
		<text x="200" y="150" text-anchor="middle" dominant-baseline="middle" font-size="16" font-weight="600" fill="var(--ink)">
			[REPLACE: Quadrant 1 Name]
		</text>
		
		<!-- Quadrant 2 (top-right) -->
		<rect x="400" y="0" width="400" height="300" fill="rgba(37, 99, 235, 0.05)" stroke="var(--line)" stroke-width="1"/>
		<text x="600" y="150" text-anchor="middle" dominant-baseline="middle" font-size="16" font-weight="600" fill="var(--ink)">
			[REPLACE: Quadrant 2 Name]
		</text>
		
		<!-- Quadrant 3 (bottom-left) -->
		<rect x="0" y="300" width="400" height="300" fill="rgba(37, 99, 235, 0.05)" stroke="var(--line)" stroke-width="1"/>
		<text x="200" y="450" text-anchor="middle" dominant-baseline="middle" font-size="16" font-weight="600" fill="var(--ink)">
			[REPLACE: Quadrant 3 Name]
		</text>
		
		<!-- Quadrant 4 (bottom-right) -->
		<rect x="400" y="300" width="400" height="300" fill="rgba(37, 99, 235, 0.05)" stroke="var(--line)" stroke-width="1"/>
		<text x="600" y="450" text-anchor="middle" dominant-baseline="middle" font-size="16" font-weight="600" fill="var(--ink)">
			[REPLACE: Quadrant 4 Name]
		</text>
		
		<!-- X-axis label -->
		<text x="750" y="580" font-size="12" fill="var(--muted)" text-anchor="middle">
			[REPLACE: X-axis Label] →
		</text>
		<text x="50" y="580" font-size="12" fill="var(--muted)" text-anchor="middle">
			← [REPLACE: X-axis Label]
		</text>
		
		<!-- Y-axis label -->
		<text x="20" y="50" font-size="12" fill="var(--muted)" text-anchor="middle" transform="rotate(-90 20 50)">
			↑ [REPLACE: Y-axis Label]
		</text>
		<text x="20" y="550" font-size="12" fill="var(--muted)" text-anchor="middle" transform="rotate(-90 20 550)">
			[REPLACE: Y-axis Label] ↓
		</text>
	</svg>
</div>
```

**Key safety rules for this template:**
- `text-anchor="middle"` + fixed `x`/`y` coordinates tied to shape centers → text is always centered, never drifts
- `viewBox="0 0 800 600"` is the source coordinate system (immutable)
- `width="800" height="600"` on the SVG tag (explicit, not computed)
- `max-width: 100%; height: auto;` on the SVG style → responsive but never distorted
- The `aspect-ratio` wrapper prevents the diagram from squishing if content reflows

### Which diagram goes in which document

| Diagram archetype | Use in | Template below |
|---|---|---|
| Opportunity Solution Tree | Card 1 (Problem/Opportunity) | Archetype C: Tree |
| Business Health Scorecard | Card 2 (Business Health) | Archetype A: 2×2 Grid |
| Competitive Positioning Map | Card 3 (Market/Competitive) | Archetype D: Scatter Plot |
| TAM/SAM/SOM | Card 4 (Value Hypothesis) | Archetype B: Concentric |
| Ansoff Matrix | Card 4 (Value Hypothesis) | Archetype A: 2×2 Grid |
| Altitude-Horizon | Card 5 (Strategic Fit) | Archetype D: Scatter Plot |
| Phased Roadmap Timeline | Card 6 (MVP/Roadmap) | Archetype E: Timeline |
| Epic Breakdown Tree | Card 6 (MVP/Roadmap) | Archetype C: Tree |
| Risk Heatmap | Card 9 (Risk & Governance) | Archetype F: Heatmap |
| Feasibility Dependency Map | Card 8 (Tech Feasibility) | Archetype C: Tree (horizontal) |
| Decision Funnel | Card 10 (Executive Deck) | Archetype G: Funnel |

---

### Archetype B: Concentric Circles (TAM/SAM/SOM)

```html
<div style="aspect-ratio: 800 / 600; max-width: 100%; margin: 1.5rem 0;">
	<svg viewBox="0 0 800 600" width="800" height="600" style="max-width: 100%; height: auto;">
		<circle cx="400" cy="300" r="260" fill="rgba(37, 99, 235, 0.08)" stroke="var(--accent)" stroke-width="2"/>
		<circle cx="400" cy="300" r="175" fill="rgba(37, 99, 235, 0.14)" stroke="var(--accent)" stroke-width="2"/>
		<circle cx="400" cy="300" r="95" fill="rgba(37, 99, 235, 0.22)" stroke="var(--accent)" stroke-width="2"/>

		<!-- Labels sit in each ring band, never on an edge -->
		<text x="400" y="80" text-anchor="middle" font-size="18" font-weight="600" fill="var(--ink)">TAM — [REPLACE: $ value]</text>
		<text x="400" y="165" text-anchor="middle" font-size="16" font-weight="600" fill="var(--ink)">SAM — [REPLACE: $ value]</text>
		<text x="400" y="295" text-anchor="middle" font-size="15" font-weight="700" fill="var(--ink)">SOM</text>
		<text x="400" y="318" text-anchor="middle" font-size="14" fill="var(--ink-soft)">[REPLACE: $ value]</text>

		<text x="400" y="560" text-anchor="middle" font-size="12" fill="var(--muted)">[REPLACE: sizing method — bottom-up / top-down / value-based]</text>
	</svg>
</div>
```

**Fixed geometry:** cx/cy always 400/300. Radii 260 / 175 / 95. Only change the label text.

---

### Archetype C: Tree / Hierarchy (OST, Epic Breakdown)

```html
<div style="aspect-ratio: 900 / 520; max-width: 100%; margin: 1.5rem 0;">
	<svg viewBox="0 0 900 520" width="900" height="520" style="max-width: 100%; height: auto;">
		<!-- Root -->
		<rect x="330" y="20" width="240" height="60" rx="6" fill="var(--card)" stroke="var(--accent)" stroke-width="2"/>
		<text x="450" y="55" text-anchor="middle" dominant-baseline="middle" font-size="15" font-weight="600" fill="var(--ink)">[REPLACE: Desired Outcome]</text>

		<!-- Connectors root -> level 2 -->
		<line x1="450" y1="80" x2="450" y2="110" stroke="var(--line)" stroke-width="2"/>
		<line x1="150" y1="110" x2="750" y2="110" stroke="var(--line)" stroke-width="2"/>
		<line x1="150" y1="110" x2="150" y2="140" stroke="var(--line)" stroke-width="2"/>
		<line x1="450" y1="110" x2="450" y2="140" stroke="var(--line)" stroke-width="2"/>
		<line x1="750" y1="110" x2="750" y2="140" stroke="var(--line)" stroke-width="2"/>

		<!-- Level 2: three nodes -->
		<rect x="40" y="140" width="220" height="56" rx="6" fill="var(--fill)" stroke="var(--line)" stroke-width="2"/>
		<text x="150" y="168" text-anchor="middle" dominant-baseline="middle" font-size="14" fill="var(--ink)">[REPLACE: Opportunity 1]</text>

		<rect x="340" y="140" width="220" height="56" rx="6" fill="var(--fill)" stroke="var(--line)" stroke-width="2"/>
		<text x="450" y="168" text-anchor="middle" dominant-baseline="middle" font-size="14" fill="var(--ink)">[REPLACE: Opportunity 2]</text>

		<rect x="640" y="140" width="220" height="56" rx="6" fill="var(--fill)" stroke="var(--line)" stroke-width="2"/>
		<text x="750" y="168" text-anchor="middle" dominant-baseline="middle" font-size="14" fill="var(--ink)">[REPLACE: Opportunity 3]</text>

		<!-- Connectors level 2 -> level 3 -->
		<line x1="150" y1="196" x2="150" y2="230" stroke="var(--line)" stroke-width="2"/>
		<line x1="450" y1="196" x2="450" y2="230" stroke="var(--line)" stroke-width="2"/>
		<line x1="750" y1="196" x2="750" y2="230" stroke="var(--line)" stroke-width="2"/>

		<!-- Level 3: solutions under each -->
		<rect x="55" y="230" width="190" height="46" rx="6" fill="var(--page)" stroke="var(--line)" stroke-width="1"/>
		<text x="150" y="253" text-anchor="middle" dominant-baseline="middle" font-size="13" fill="var(--ink-soft)">[REPLACE: Solution 1a]</text>
		<rect x="55" y="286" width="190" height="46" rx="6" fill="var(--page)" stroke="var(--line)" stroke-width="1"/>
		<text x="150" y="309" text-anchor="middle" dominant-baseline="middle" font-size="13" fill="var(--ink-soft)">[REPLACE: Solution 1b]</text>

		<rect x="355" y="230" width="190" height="46" rx="6" fill="var(--page)" stroke="var(--line)" stroke-width="1"/>
		<text x="450" y="253" text-anchor="middle" dominant-baseline="middle" font-size="13" fill="var(--ink-soft)">[REPLACE: Solution 2a]</text>
		<rect x="355" y="286" width="190" height="46" rx="6" fill="var(--page)" stroke="var(--line)" stroke-width="1"/>
		<text x="450" y="309" text-anchor="middle" dominant-baseline="middle" font-size="13" fill="var(--ink-soft)">[REPLACE: Solution 2b]</text>

		<rect x="655" y="230" width="190" height="46" rx="6" fill="var(--page)" stroke="var(--line)" stroke-width="1"/>
		<text x="750" y="253" text-anchor="middle" dominant-baseline="middle" font-size="13" fill="var(--ink-soft)">[REPLACE: Solution 3a]</text>
		<rect x="655" y="286" width="190" height="46" rx="6" fill="var(--page)" stroke="var(--line)" stroke-width="1"/>
		<text x="750" y="309" text-anchor="middle" dominant-baseline="middle" font-size="13" fill="var(--ink-soft)">[REPLACE: Solution 3b]</text>
	</svg>
</div>
```

**Fixed geometry:** three columns centered at x = 150 / 450 / 750. To use fewer branches, delete a whole column (rect + text + connector) — never reposition the remaining ones.

---

### Archetype D: Scatter / 2-Axis Plot (Positioning Map, Altitude-Horizon)

```html
<div style="aspect-ratio: 800 / 600; max-width: 100%; margin: 1.5rem 0;">
	<svg viewBox="0 0 800 600" width="800" height="600" style="max-width: 100%; height: auto;">
		<!-- Plot area -->
		<rect x="90" y="40" width="660" height="460" fill="var(--fill)" stroke="var(--line)" stroke-width="1"/>

		<!-- Axes -->
		<line x1="90" y1="500" x2="750" y2="500" stroke="var(--ink-soft)" stroke-width="2"/>
		<line x1="90" y1="40" x2="90" y2="500" stroke="var(--ink-soft)" stroke-width="2"/>

		<!-- Midlines (optional quadrant split) -->
		<line x1="420" y1="40" x2="420" y2="500" stroke="var(--line)" stroke-width="1" stroke-dasharray="4 4"/>
		<line x1="90" y1="270" x2="750" y2="270" stroke="var(--line)" stroke-width="1" stroke-dasharray="4 4"/>

		<!-- Plotted points: change cx/cy ONLY using the grid guide below -->
		<circle cx="580" cy="160" r="9" fill="var(--accent-strong)"/>
		<text x="580" y="140" text-anchor="middle" font-size="13" font-weight="600" fill="var(--ink)">[REPLACE: Us]</text>

		<circle cx="250" cy="200" r="9" fill="var(--muted)"/>
		<text x="250" y="180" text-anchor="middle" font-size="13" fill="var(--ink-soft)">[REPLACE: Competitor A]</text>

		<circle cx="330" cy="400" r="9" fill="var(--muted)"/>
		<text x="330" y="380" text-anchor="middle" font-size="13" fill="var(--ink-soft)">[REPLACE: Competitor B]</text>

		<circle cx="640" cy="410" r="9" fill="var(--muted)"/>
		<text x="640" y="390" text-anchor="middle" font-size="13" fill="var(--ink-soft)">[REPLACE: Competitor C]</text>

		<!-- Axis labels -->
		<text x="420" y="545" text-anchor="middle" font-size="13" font-weight="600" fill="var(--muted)">[REPLACE: X-axis — low → high]</text>
		<text x="30" y="270" text-anchor="middle" font-size="13" font-weight="600" fill="var(--muted)" transform="rotate(-90 30 270)">[REPLACE: Y-axis — low → high]</text>
	</svg>
</div>
```

**Positioning guide — use these values only.** Plot area spans x 90→750, y 40→500 (y is inverted: smaller y = higher value).

| Position | cx | cy |
|---|---|---|
| Low / Low | 250 | 410 |
| Low / High | 250 | 160 |
| Mid / Mid | 420 | 270 |
| High / Low | 610 | 410 |
| High / High | 610 | 160 |

Always place the label 20px above its circle (`y = cy - 20`).

---

### Archetype E: Timeline / Swimlane (Phased Roadmap)

```html
<div style="aspect-ratio: 900 / 380; max-width: 100%; margin: 1.5rem 0;">
	<svg viewBox="0 0 900 380" width="900" height="380" style="max-width: 100%; height: auto;">
		<!-- Phase bars -->
		<rect x="40" y="60" width="240" height="70" rx="6" fill="rgba(37, 99, 235, 0.22)" stroke="var(--accent)" stroke-width="2"/>
		<text x="160" y="88" text-anchor="middle" font-size="15" font-weight="600" fill="var(--ink)">[REPLACE: Phase 1 — MVP]</text>
		<text x="160" y="110" text-anchor="middle" font-size="12" fill="var(--ink-soft)">[REPLACE: scope summary]</text>

		<rect x="300" y="60" width="260" height="70" rx="6" fill="rgba(37, 99, 235, 0.14)" stroke="var(--accent)" stroke-width="2"/>
		<text x="430" y="88" text-anchor="middle" font-size="15" font-weight="600" fill="var(--ink)">[REPLACE: Phase 2 — Fast Follow]</text>
		<text x="430" y="110" text-anchor="middle" font-size="12" fill="var(--ink-soft)">[REPLACE: scope summary]</text>

		<rect x="580" y="60" width="280" height="70" rx="6" fill="rgba(37, 99, 235, 0.08)" stroke="var(--accent)" stroke-width="2"/>
		<text x="720" y="88" text-anchor="middle" font-size="15" font-weight="600" fill="var(--ink)">[REPLACE: Phase 3 — Scale]</text>
		<text x="720" y="110" text-anchor="middle" font-size="12" fill="var(--ink-soft)">[REPLACE: scope summary]</text>

		<!-- Timeline axis -->
		<line x1="40" y1="200" x2="860" y2="200" stroke="var(--ink-soft)" stroke-width="2"/>

		<!-- Milestone markers (aligned to phase boundaries) -->
		<circle cx="280" cy="200" r="7" fill="var(--accent-strong)"/>
		<text x="280" y="232" text-anchor="middle" font-size="12" fill="var(--ink)">[REPLACE: Gate 1 date]</text>
		<text x="280" y="250" text-anchor="middle" font-size="11" fill="var(--muted)">[REPLACE: go/no-go criteria]</text>

		<circle cx="560" cy="200" r="7" fill="var(--accent-strong)"/>
		<text x="560" y="232" text-anchor="middle" font-size="12" fill="var(--ink)">[REPLACE: Gate 2 date]</text>
		<text x="560" y="250" text-anchor="middle" font-size="11" fill="var(--muted)">[REPLACE: go/no-go criteria]</text>

		<circle cx="860" cy="200" r="7" fill="var(--accent-strong)"/>
		<text x="830" y="232" text-anchor="middle" font-size="12" fill="var(--ink)">[REPLACE: Target date]</text>
	</svg>
</div>
```

**Fixed geometry:** phase bars occupy x 40–280, 300–560, 580–860. Milestone circles sit at the boundaries (280 / 560 / 860). Opacity decreases left→right to signal decreasing certainty — keep that.

---

### Archetype F: Heatmap Grid (Risk Assessment)

```html
<div style="aspect-ratio: 700 / 560; max-width: 100%; margin: 1.5rem 0;">
	<svg viewBox="0 0 700 560" width="700" height="560" style="max-width: 100%; height: auto;">
		<!-- Row 3 (High likelihood) -->
		<rect x="120" y="40" width="180" height="140" fill="#fff3bf" stroke="var(--line)" stroke-width="1"/>
		<rect x="300" y="40" width="180" height="140" fill="#ffc9c9" stroke="var(--line)" stroke-width="1"/>
		<rect x="480" y="40" width="180" height="140" fill="#ffa8a8" stroke="var(--line)" stroke-width="1"/>
		<!-- Row 2 (Medium) -->
		<rect x="120" y="180" width="180" height="140" fill="#d3f9d8" stroke="var(--line)" stroke-width="1"/>
		<rect x="300" y="180" width="180" height="140" fill="#fff3bf" stroke="var(--line)" stroke-width="1"/>
		<rect x="480" y="180" width="180" height="140" fill="#ffc9c9" stroke="var(--line)" stroke-width="1"/>
		<!-- Row 1 (Low) -->
		<rect x="120" y="320" width="180" height="140" fill="#d3f9d8" stroke="var(--line)" stroke-width="1"/>
		<rect x="300" y="320" width="180" height="140" fill="#d3f9d8" stroke="var(--line)" stroke-width="1"/>
		<rect x="480" y="320" width="180" height="140" fill="#fff3bf" stroke="var(--line)" stroke-width="1"/>

		<!-- Plotted risks: use ONLY the 9 cell-center coordinates listed below -->
		<circle cx="570" cy="110" r="10" fill="#1e1e1e"/>
		<text x="570" y="115" text-anchor="middle" font-size="11" font-weight="700" fill="#ffffff">1</text>

		<circle cx="390" cy="250" r="10" fill="#1e1e1e"/>
		<text x="390" y="255" text-anchor="middle" font-size="11" font-weight="700" fill="#ffffff">2</text>

		<circle cx="210" cy="390" r="10" fill="#1e1e1e"/>
		<text x="210" y="395" text-anchor="middle" font-size="11" font-weight="700" fill="#ffffff">3</text>

		<!-- Y axis labels -->
		<text x="105" y="110" text-anchor="end" font-size="13" fill="var(--ink)">High</text>
		<text x="105" y="250" text-anchor="end" font-size="13" fill="var(--ink)">Med</text>
		<text x="105" y="390" text-anchor="end" font-size="13" fill="var(--ink)">Low</text>
		<text x="40" y="250" text-anchor="middle" font-size="13" font-weight="600" fill="var(--muted)" transform="rotate(-90 40 250)">Likelihood</text>

		<!-- X axis labels -->
		<text x="210" y="485" text-anchor="middle" font-size="13" fill="var(--ink)">Low</text>
		<text x="390" y="485" text-anchor="middle" font-size="13" fill="var(--ink)">Med</text>
		<text x="570" y="485" text-anchor="middle" font-size="13" fill="var(--ink)">High</text>
		<text x="390" y="520" text-anchor="middle" font-size="13" font-weight="600" fill="var(--muted)">Impact</text>
	</svg>
</div>
```

**Cell centers — plot risk dots at these coordinates only:**

| | Impact Low (cx 210) | Impact Med (cx 390) | Impact High (cx 570) |
|---|---|---|---|
| **Likelihood High** (cy 110) | amber | red | dark red |
| **Likelihood Med** (cy 250) | green | amber | red |
| **Likelihood Low** (cy 390) | green | green | amber |

Number each dot and key it to a table in the document body (`1 = [risk name] → [mitigation]`). Do not put risk names inside the dots. Cell fills are semantic — never recolor them.

---

### Archetype G: Funnel (Executive Decision Flow)

```html
<div style="aspect-ratio: 700 / 560; max-width: 100%; margin: 1.5rem 0;">
	<svg viewBox="0 0 700 560" width="700" height="560" style="max-width: 100%; height: auto;">
		<rect x="60" y="30" width="580" height="70" rx="4" fill="rgba(37, 99, 235, 0.28)" stroke="var(--accent)" stroke-width="2"/>
		<text x="350" y="70" text-anchor="middle" dominant-baseline="middle" font-size="16" font-weight="600" fill="var(--ink)">1 · Problem — [REPLACE: one line]</text>

		<rect x="110" y="115" width="480" height="70" rx="4" fill="rgba(37, 99, 235, 0.24)" stroke="var(--accent)" stroke-width="2"/>
		<text x="350" y="155" text-anchor="middle" dominant-baseline="middle" font-size="16" font-weight="600" fill="var(--ink)">2 · Market — [REPLACE: one line]</text>

		<rect x="160" y="200" width="380" height="70" rx="4" fill="rgba(37, 99, 235, 0.20)" stroke="var(--accent)" stroke-width="2"/>
		<text x="350" y="240" text-anchor="middle" dominant-baseline="middle" font-size="16" font-weight="600" fill="var(--ink)">3 · Strategy — [REPLACE: one line]</text>

		<rect x="210" y="285" width="280" height="70" rx="4" fill="rgba(37, 99, 235, 0.16)" stroke="var(--accent)" stroke-width="2"/>
		<text x="350" y="325" text-anchor="middle" dominant-baseline="middle" font-size="16" font-weight="600" fill="var(--ink)">4 · Plan — [REPLACE: one line]</text>

		<rect x="245" y="370" width="210" height="70" rx="4" fill="rgba(37, 99, 235, 0.12)" stroke="var(--accent)" stroke-width="2"/>
		<text x="350" y="410" text-anchor="middle" dominant-baseline="middle" font-size="16" font-weight="600" fill="var(--ink)">5 · Viability</text>

		<rect x="270" y="455" width="160" height="70" rx="4" fill="var(--accent-strong)" stroke="var(--accent-strong)" stroke-width="2"/>
		<text x="350" y="495" text-anchor="middle" dominant-baseline="middle" font-size="17" font-weight="700" fill="#ffffff">6 · DECISION</text>
	</svg>
</div>
```

**Fixed geometry:** every bar is centered on x=350 and 70px tall, spaced 85px apart vertically. Widths narrow 580 → 480 → 380 → 280 → 210 → 160. Never change the x/width pairs — they are precomputed to stay centered.

---

### Failure Modes & Fixes

| What goes wrong | Why | Fix |
|---|---|---|
| Text drifts outside the box | ChatGPT recalculated `x`/`y` position | Use fixed `x`/`y` tied to shape center; only let ChatGPT change text content |
| Quadrants look squished | `aspect-ratio` not set, SVG stretches | Add `aspect-ratio: W / H` wrapper div |
| Diagram looks tiny on mobile | SVG has fixed `width="800"` but no responsive fallback | Add `max-width: 100%; height: auto;` style on `<svg>` |
| Colors don't change in dark mode | Hardcoded `#000000` or `#FFFFFF` | Use `var(--ink)`, `var(--card)`, `var(--accent)` CSS variables |
| Grid lines are blurry | Fractional coordinates | Use integer coordinates for lines and shapes |
| Funnel bars drift off-center | Widths edited without recomputing `x` | Use the precomputed width/x pairs in Archetype G verbatim |
| Scatter dots land outside the plot | Coordinates invented | Use only the coordinates in the Archetype D positioning table |
| Long label overflows its box | Text longer than the shape width | Shorten the label — never widen the shape |

---

### The instruction to give ChatGPT-5 when requesting a diagram

Paste this alongside your request:

```
Use the SVG template for [ARCHETYPE NAME] from Part 3.5 exactly as written.
Substitute ONLY the [REPLACE: ...] text content.
Do not change any x, y, cx, cy, width, height, r, or viewBox value.
Do not add or remove shapes unless the template says a whole column/row may be deleted.
```

That instruction is what holds alignment at ~95% reliability. Without it, ChatGPT recalculates coordinates and the layout drifts.

---

## Part 3.6: Optional Humanizer Pass

**This part is OFF by default.** Parts 1–3.5 already produce direct, evidence-based, active-voice prose — that discipline covers most of what makes writing sound "AI-generated" in the first place. Only run this section when the request explicitly asks for it.

### Trigger phrases

Apply this pass only when the request includes something like: **"humanize this"**, **"make it sound human"**, **"--humanize"**, **"run the humanizer pass"**, or a standalone follow-up like **"humanize the document above"** / **"humanize the last document."**

**No flag → skip this part entirely.** Output the document exactly as Parts 0–3.5 specify, nothing more.

### When to apply it in the flow

**Never bundle humanizing into the same reasoning step as generating the document.** If a single request asks for both (e.g., "create the Problem-Opportunity Assessment and humanize it"), treat it as two clearly separate passes within your response:

1. First, generate the complete document per its Part 3 card and the Part 2 template — exactly as you would with no flag.
2. Only after that document is fully built, apply this section as a distinct second pass, rewriting the prose inside it.

Keeping these separate (rather than trying to write "humanized" prose from scratch in one blended step) keeps each pass simpler and less likely to trip a capability limit. This also works cleanly as two separate messages — generate now, "humanize the above" later — which is the safer pattern if the document itself is already complex (e.g., it has an embedded diagram).

**What actually changes:** only the prose inside `<p>`, `<li>`, `<h3>`, `.card p`, header/footer text nodes, and similar text content. Never touch the CSS, the SVG coordinates, the HTML tag structure, or any `[REPLACE: ...]` mechanics from Parts 2–3.5 — this pass rewrites words, not structure.

### Core invariant rules (apply every time this pass runs)

1. **Identify AI patterns** — scan the generated prose for the patterns listed below.
2. **Preserve every claim** — every fact, number, and quote in the original document survives into the rewrite. Compress the dull parts, dwell where a director would want detail, merge or split sentences freely — but no fact drops out.
3. **Never invent facts.** The rewrite must not introduce any number, name, date, quote, or citation that wasn't already in the document. If a vague-sounding phrase needs a specific replacement, the specific must already exist elsewhere in the document's own content (e.g., a stat already stated in another section) — otherwise cut the vague claim rather than inventing a specific one to replace it. This is the single most important rule for a fact-heavy document stack: **fixing "Industry reports suggest churn is high" means citing the churn number already in the document, or cutting the sentence — never fabricating a source or a number that wasn't there.**
4. **Match the voice to the section type** (judgment call below) — don't apply the same tone uniformly across a document that has both technical tables and a persuasive recommendation.

### The judgment call: when neutral is correct vs. when voice is appropriate

- **Technical/reference sections stay neutral.** PRD requirements tables, Feasibility risk tables, Risk Heatmap entries, metric definitions, MoSCoW categorization — for these, plain and neutral language *is* the correct humanized output. Do not add opinion, first-person voice, or stylistic flourish here; a Risk table with "editorializing" is worse, not better.
- **Persuasive/narrative sections can carry voice.** The Executive Decision Deck's headline and recommendation, the Strategic Fit Memo's positioning statement, the Problem/Opportunity Statement's framing narrative — these can take directness, mild stance, and uneven sentence rhythm where the evidence already in the document supports it. Never use this license to add a claim, only to change how an already-true claim is phrased.

### The patterns (condensed — 1 example each)

**Content patterns:**

1. **Undue emphasis on significance/legacy.** Watch for: "marks a pivotal moment," "represents a shift," "underscores its importance," "sets the stage for."
   - Before: *"This initiative marks a pivotal moment in the company's onboarding evolution."*
   - After: *"This changes how we onboard enterprise customers."*

2. **Undue emphasis on notability/coverage.** Watch for: listing sources or credentials without real context, just to sound authoritative.
   - Before: *"Multiple industry analysts and press outlets have covered this trend."*
   - After: cite the one real source with real context, or cut the sentence.

3. **Superficial "-ing" analyses.** Watch for: sentences padded with trailing "-ing" phrases that add length, not information.
   - Before: *"We reduced onboarding time, reflecting our commitment to customer success and showcasing operational excellence."*
   - After: *"We reduced onboarding time from 35 to 10 days."*

4. **Promotional/advertisement language.** Watch for: "robust," "seamless," "cutting-edge," "best-in-class," "game-changing."
   - Before: *"Our seamless, best-in-class integration delivers a game-changing experience."*
   - After: *"The integration connects to Salesforce and HubSpot without manual setup."*

5. **Vague attributions/weasel words.** Watch for: "industry reports suggest," "experts believe," "studies show" with no named source.
   - Before: *"Industry reports suggest churn is a growing concern."*
   - After: *"Churn increased from 8% to 12.5% this quarter"* (using the number already in the document) — or cut the sentence if no real number exists.

6. **Formulaic "Challenges and Future Prospects" sections.** Watch for: generic "despite challenges, we remain optimistic" closers that say nothing specific.
   - Before: *"Despite these challenges, we remain confident in our path forward."*
   - After: name the actual next decision point and what would trigger it, or cut the sentence.

**Language/grammar patterns:**

7. **Overused AI vocabulary.** Watch for: *crucial, delve, leverage, robust, seamless, foster, unlock, elevate, landscape (as abstract noun), tapestry, testament, underscore (as verb), pivotal, vibrant.*
   - Before: *"This is a crucial, pivotal capability that will unlock seamless growth."*
   - After: *"This capability lets sales close deals 2 weeks faster."*

8. **Copula avoidance.** Watch for: "serves as," "stands as," "functions as" instead of a plain "is."
   - Before: *"This dashboard serves as the primary source of truth for retention metrics."*
   - After: *"This dashboard is the primary source for retention metrics."*

9. **Negative parallelisms / tailing negations.** Watch for: "not only X but Y," "it's not just about X, it's Y," or a clause tacked on with "no X" at the end.
   - Before: *"This isn't just a metrics dashboard, it's a strategic decision engine."*
   - After: *"This dashboard drives the quarterly resourcing decision."*

10. **Rule of three overuse.** Watch for: forcing every list into exactly three items to sound comprehensive, even when two or four items are the actual truth.
    - Before: *"This delivers speed, scale, and simplicity."*
    - After: state the two real benefits the evidence actually supports.

11. **Elegant variation (synonym cycling).** Watch for: swapping in a new synonym for the same referent every sentence ("the platform... the tool... the solution...") to avoid repetition.
    - Before: *"The platform reduces friction. The tool simplifies onboarding. The solution scales with the team."*
    - After: *"The platform reduces friction, simplifies onboarding, and scales with the team."*

12. **Passive voice / subjectless fragments.** Watch for: hiding the actor — "it was determined," "no action is required."
    - Before: *"It was found that churn increased in Q3."*
    - After: *"Churn increased in Q3."*

13. **Em dashes — cut them.** The final rewrite contains no em dashes (—) or en dashes (–). Replace with a period, comma, colon, or parentheses depending on what the sentence needs.
    - Before: *"The rollout — originally planned for Q2 — slipped to Q3."*
    - After: *"The rollout, originally planned for Q2, slipped to Q3."*

14. **Overuse of boldface.** Watch for: mechanically bolding every key term in a list, which defeats the purpose of emphasis.
    - Before: *"We improved **retention**, **NPS**, and **time-to-value**."*
    - After: *"We improved retention, NPS, and time-to-value."* (bold only the one number a director should actually notice, if any)

### Output instruction

After applying the pass, re-output the complete HTML document — same structure, same CSS, same diagrams — with only the prose rewritten. Scan the final output for em dashes (`—`, `–`) before returning it; any hit means the pass isn't done.

---

## Part 4: Document Sequencing Guidance

**Read and create documents in this order.** Each feeds into the next.

1. **Card 1: Problem/Opportunity** — Proves the problem exists and sizing
2. **Card 2: Business Health Diagnostic** — Current state baseline (for context)
3. **Card 3: Market/Competitive Intelligence** — Competitive landscape and positioning
4. **Card 4: Value Hypothesis & Sizing** — TAM/SAM/SOM, growth quadrant
5. **Card 5: Strategic Fit Memo** — Does this align with strategy?
6. **Card 6: MVP/Roadmap Proposal** — How we'll build it (phases)
7. **Card 7: PRD** — Detailed spec for Phase 1
8. **Card 8: Technical Feasibility** — Can we actually do this?
9. **Card 9: Risk & Governance** — What could go wrong?
10. **Card 10: Executive Decision Deck** — Synthesis of all above; the ask

**Why this order:**
- Each document adds information that downstream docs need
- Cards 1-5 build the *case* (this is worth doing)
- Cards 6-9 build the *plan* (here's how we'll do it)
- Card 10 synthesizes into a single clear ask

**If you're short on time:** Card 1 + Card 4 + Card 10 is a lean case. Add Card 8 (feasibility) if risk matters.

**Where the operational and delivery skills (Parts 6–7) fit in:** these aren't part of the sequence above — they're skills you reach for at any point in the product lifecycle, not just during a decision case. Card 16 (Epic Hypothesis) and Card 17 (Epic Breakdown Advisor) commonly sit right before or inside Card 6 (turning the roadmap's Phase 1 into a validated, properly-sized slice). Card 11 (Metrics Review), Card 14 (Sprint Planning), and Card 15 (Stakeholder Update) are recurring operational cadences, not one-time deliverables. Card 12 (Product Brainstorming) can precede Card 1 (finding the problem worth writing up) or run standalone anytime you need a thinking partner. Card 13 (Roadmap Update) is what you reach for after Card 6's roadmap exists and needs to change.

---

## Part 5: Master Prompt Template for ChatGPT-5

**Use this pattern every time you ask for a document or skill.**

```
Using the Product Management Assistant Knowledge Base above, create the [DOCUMENT OR SKILL NAME].

Here's what I know so far:
- [Your inputs: product, problem, data, context]
- [Any constraints: timeline, budget, team size]
- [Any relevant prior docs: "see Business Health Diagnostic above"]

Ask me only for what's missing from the Required Inputs list for this type.
```

### Example 1: Business Health Diagnostic

```
Using the Product Management Assistant Knowledge Base above, create the Business Health Diagnostic.

Here's what I know:
- $8M ARR, growing 60% YoY
- NRR 96%, monthly churn 4%
- CAC $15K, LTV $180K (payback 13 months)
- 14 months runway, burning $200K/month
- Board meeting in 3 weeks

Ask me only for what's missing from the Required Inputs list.
```

### Example 2: Executive Decision Deck

```
Using the Product Management Assistant Knowledge Base above, create the Executive Decision Deck.

I have these documents completed:
1. Problem/Opportunity Statement (attached above)
4. Value Hypothesis & Sizing (attached above)
6. MVP/Roadmap Proposal (attached above)
8. Technical Feasibility Assessment (attached above)

Here's the investment ask: $400K team cost, 4-month timeline, targeting $2.4M ARR by year-end.

Create the deck synthesizing all above into a Go/No-Go recommendation.
```

### Example 3: With the optional humanizer flag

```
Using the Product Management Assistant Knowledge Base above, create the Problem-Opportunity Assessment.

Here's what I know:
- [inputs...]

Once the document is complete, apply the Humanizer Pass (Part 3.6) to the output.
```

Or as a standalone follow-up in a later turn, once a document already exists in the conversation:

```
Humanize the document above.
```

### Example 4: Sprint Planning (Card 14)

```
Using the Product Management Assistant Knowledge Base above, run a Sprint Planning session (Card 14).

Team: 4 engineers, sprint length 2 weeks.
Backlog: [paste or describe]
Carryover from last sprint: [describe, or say "none"]

Ask me only for what's missing before producing the sprint plan.
```

### Example 5: Epic Breakdown Advisor (Card 17)

```
Using the Product Management Assistant Knowledge Base above, use the Epic Breakdown Advisor (Card 17) on this epic:

"[paste the epic/backlog item as written]"

Walk it through the INVEST check and the 9 splitting patterns in order, and tell me which pattern applies.
```

---

## Part 6: Operational PM Skills

Five recurring, real-world PM workflows. Unlike Cards 1-10, most of these aren't one-time decision documents — they're skills you come back to on a cadence (weekly metrics, every sprint, every stakeholder update) or on demand (a brainstorm, a roadmap change). Each card below notes its own output shape; not all of them use the Part 2 HTML template.

**Fuller worked examples for all 5 skills below are in the companion file, `Product-Management-Assistant-Examples.md`** — upload it alongside this file for a complete filled-in sample of each skill in action.

---

### Card 11: Metrics Review

**Trigger phrases:** "metrics review", "review our metrics", "how are we doing", "KPI review", "weekly/monthly/quarterly metrics check", "investigate this spike/drop"

**Core question it answers:** How healthy is the product right now, and what should we do about what changed?

**Required inputs:**
- Time period to review (last week, last month, last quarter)
- The metrics and their values (paste a table, describe, or say which ones to focus on)
- Comparison data (previous period, targets, if available)
- Any known events that might explain changes (launches, outages, marketing campaigns, seasonality)

**Interaction mode:** Document-shaped output (Scorecard table + narrative sections). Can use the Part 2 HTML template for a polished version, or plain markdown for a quick check-in — ask which the user wants if unclear.

**Output structure:**

1. **Summary** — 2-3 sentences: overall product health, most notable change, key callout
2. **Metric Scorecard** — table: Metric | Current | Previous | Change | Target | Status (On track / At risk / Miss)
3. **Trend Analysis** — for each metric worth discussing: what happened, why it likely happened (attribution based on known events or correlated metrics), whether it's one-time or sustained
4. **Bright Spots** — metrics beating targets, positive trends to sustain
5. **Areas of Concern** — metrics missing targets or trending negatively, early warning signals
6. **Recommended Actions** — investigations to run, experiments to launch, investments to make, alerts to set
7. **Context and Caveats** — known data quality issues, events affecting comparability, gaps in tracking

**Reasoning:**
- A metrics review is only useful if it changes what the team does next — a review that ends without at least one recommended action wasn't worth running
- Absolute numbers without comparison are meaningless; always show current vs. previous vs. target
- Segment analysis often reveals that a flat aggregate number is hiding one segment growing and another shrinking

**Skill source:** [metrics-review](https://github.com/anthropics/knowledge-work-plugins/tree/main/product-management/skills/metrics-review)

**Product Metrics Hierarchy (embedded):**

- **North Star Metric:** the single metric that best captures the core value delivered to users. Should be value-aligned (moves when users get more value), leading (predicts long-term business success), actionable (team can influence it), and understandable (everyone in the company gets what it means). Examples by product type: collaboration tool → weekly active teams with 3+ contributors; marketplace → weekly transactions completed; SaaS platform → weekly active users completing the core workflow.

- **L1 Metrics (Health Indicators)** mapped to lifecycle stage:
  - **Acquisition:** new signups/trial starts, signup conversion rate, channel mix, cost per acquisition
  - **Activation:** activation rate (% completing the key action that predicts retention), time to activate, setup completion rate
  - **Engagement:** DAU/WAU/MAU, DAU/MAU ratio (stickiness — above 0.5 = daily habit, below 0.2 = infrequent), core action frequency, feature adoption
  - **Retention:** D1/D7/D30 retention, cohort retention curves, churn rate, resurrection rate
  - **Monetization:** free-to-paid conversion, MRR/ARR, ARPU/ARPA, expansion revenue, net revenue retention
  - **Satisfaction:** NPS, CSAT, support ticket volume/resolution time, app store ratings

- **L2 Metrics (Diagnostic):** funnel conversion at each step, feature-level usage, segment breakdowns (plan, company size, geography, role), performance metrics, content-specific engagement — used to investigate changes in L1.

**OKR framework (embedded, for setting the targets a Metrics Review checks against):**
- **Objectives:** qualitative, aspirational, time-bound, directional (not metric-specific)
- **Key Results:** quantitative, time-bound, outcome-based (not output-based), 2-4 per objective
- **Best practices:** 70% completion is the target for a good stretch OKR (100% every time means targets weren't ambitious enough); grade honestly at period end — 0.0-0.3 = missed, 0.4-0.6 = progress, 0.7-1.0 = achieved; do not run more than 2-3 objectives with 2-4 KRs each

**Review cadences (embedded):**
- **Weekly** (15-30 min, PM + maybe eng lead): North Star + key L1 movements, active experiment results, anomalies, alerts. Action: investigate anything off, otherwise note and move on.
- **Monthly** (30-60 min, product team + stakeholders): full L1 scorecard with month-over-month trends, progress vs. quarterly OKRs, cohort analysis, feature adoption, segment divergence. Action: identify 1-3 areas to investigate or invest in.
- **Quarterly** (60-90 min, product/eng/design/leadership): OKR scoring, full-quarter trend analysis, year-over-year comparisons, competitive context. Action: set next quarter's OKRs.

**Dashboard anti-patterns to flag if the user's tracking has them:**
- Vanity metrics (total signups ever, total page views — always go up, don't indicate health)
- Too many metrics (if it doesn't fit on one screen, cut metrics)
- No comparison (raw numbers with no previous period or target)
- Stale dashboards (not reviewed in months)
- Output dashboards (measuring team activity — tickets closed, PRs merged — instead of user/business outcomes)
- One dashboard for all audiences (executives, PMs, and engineers need different views)

**Common mistakes:**
- Reporting a metric miss without a recommended action attached
- Treating every small fluctuation as signal instead of noise
- Attribution stated as fact when it's actually a correlation guess (acknowledge uncertainty)
- Segment-masking: an aggregate number that hides one segment growing and another shrinking

---

### Card 12: Product Brainstorming

**Trigger phrases:** "let's brainstorm", "help me think through this", "I need a thinking partner", "explore this problem space", "stress-test this idea", "what else could solve this"

**Core question it answers:** What are we not seeing yet, and which direction is actually worth committing to?

**Required inputs:** None strictly required — this skill can start from a vague area of interest. Useful context if available: the problem area or idea already in mind, any prior research or data, and what stage of thinking this is (just exploring vs. about to decide).

**Interaction mode: this is the one skill in this file that is NOT a document generator.** Do not produce a finished HTML deliverable or markdown report. This is a live, back-and-forth conversation where you act as a sharp thinking partner — opinionated, pushing back, asking the next question — not a stenographer producing a clean write-up. If the user wants a captured summary at the end, offer it as a final, optional step, not the primary output.

**Modes (pick based on where the conversation actually is):**

- **Problem Exploration** — user has a problem area but hasn't defined what to solve. Map the ecosystem: who's involved, what triggers the problem, what happens if nothing changes. Distinguish symptoms from root causes by repeatedly asking "why." Ask: "What happens if we do nothing? Who suffers and how?" "Who has solved a version of this problem in a different context?"

- **Solution Ideation** — problem is defined, need multiple candidate solutions. Generate 5-7 distinct approaches before evaluating any of them. Vary along scope (small tweak vs. big bet), approach (product vs. process vs. policy), timing (quick win vs. long-term). Always include one "what if we did the opposite?" option and one option that removes something rather than adds. Resist the user latching onto the first decent idea — push for more.

- **Assumption Testing** — user has a direction and needs it stress-tested. List every assumption (stated and unstated) it depends on. For each: how confident are we, what evidence do we have, what would disprove it? Identify the single riskiest assumption (the one that kills the idea if wrong) and the cheapest way to test it before building anything.

- **Strategy Exploration** — user is thinking about direction or positioning, not a single feature. Map the playing field of possible strategic moves. Think in bets: what's the payoff, what are the odds. Consider second-order effects and competitor response. Frame in timeframes: right move for 3 months vs. 12 months vs. 3 years.

**Frameworks to reach for when useful (don't force all of them into every conversation):**
- **How Might We (HMW):** reframe a pain point as an opportunity question. Structure: "How might we [outcome] for [user] without [constraint]?" Generate 5-10 variants from one problem statement — each reframing opens a different solution space.
- **Jobs-to-be-Done (JTBD):** think from the user's job, not features or demographics. Structure: "When [situation], I want to [motivation] so I can [outcome]." Ask what they "fired" to hire your product — reveals the real competitive set.
- **Opportunity Solution Tree:** Desired Outcome → Opportunities (from research, not imagination) → multiple Solutions per opportunity → Experiments per solution. See Card 1 for the fuller embedded framework.

**Session structure (Frame → Diverge → Provoke → Converge → Capture):**
1. **Frame** — what are we exploring, why now, what do we already know, what would a great outcome look like. Spend real time here; a poorly framed brainstorm produces disconnected ideas.
2. **Diverge** — generate many ideas, no judgment yet. Push past the first 3-5 ideas (those are the obvious ones anyone would think of).
3. **Provoke** — challenge what's on the table: "What's the strongest argument against this?" "Who would hate this and why?" "What is the 10x-more-ambitious version?"
4. **Converge** — group into themes, evaluate against user impact/feasibility/strategic fit/evidence strength. Don't kill an idea by committee if the user is excited about it and it's worth exploring further, even if risky.
5. **Capture** — key ideas and why they're interesting, assumptions to test, questions to research, suggested next steps, and what was explicitly set aside.

**Do:**
- Be opinionated ("I think approach B is stronger because...") rather than neutral pros/cons lists
- Challenge constructively ("That assumes X — are we confident?") not dismissively ("That won't work")
- Ask the next question when the user finishes a thought — don't just agree and move on
- Name the pattern when you see a common trap (solutioning too early, feature-parity thinking, scope creep)

**Don't:**
- Dump every framework into one conversation — use what actually helps
- Hand over a finished list and call it done — brainstorming is a conversation
- Agree with everything — a thinking partner who only validates isn't one
- Evaluate feasibility while still in divergent mode — that kills the ideation

**Common mistakes (anti-patterns to name if you see them):**
- **Solutioning before framing** — user jumps to "we should build X" before the problem is defined. Slow down, ask what problem X solves and how we know.
- **Feature parity trap** — "competitor has X, so we need X" is copying, not brainstorming. Ask what user need X actually serves.
- **The one-idea brainstorm** — user arrives with a solution and calls it a brainstorm. Acknowledge it, then push for genuine alternatives.
- **Analysis paralysis** — too much divergence, no convergence. Prompt: "If you had to pick one direction right now, which would it be and why?"

---

### Card 13: Roadmap Update

**Trigger phrases:** "update the roadmap", "reprioritize", "add this to the roadmap", "build a Now/Next/Later view", "move the timeline", "what should we cut"

**Core question it answers:** What's on the roadmap, what should change, and what's the tradeoff?

**Required inputs:**
- Current roadmap (paste, describe, or upload — any format: list, table, spreadsheet, prose)
- The operation: add an item, update status, reprioritize, move a timeline, or build a new roadmap from scratch
- For adds: name, description, priority, estimated effort, target timeframe, owner, dependencies
- For reprioritization: what changed (new information, strategy shift, resource change, customer feedback)

**Interaction mode:** Operation-based. Determine which of the 5 operations the user wants before generating anything. Output is typically a markdown table (Now/Next/Later or quarterly view), not the Part 2 HTML template — offer the HTML version only if the user wants a polished, presentable artifact.

**The 5 operations:**
1. **Add item** — gather name/description/priority/effort/timeframe/owner/dependencies, suggest where it fits given current priorities and capacity. **Always ask what comes off** — roadmaps are zero-sum against capacity.
2. **Update status** — options: not started, in progress, at risk, blocked, completed, cut. For "at risk"/"blocked": ask for the blocker and mitigation plan.
3. **Reprioritize** — ask what changed, apply a prioritization framework (below) if helpful, show a before/after comparison.
4. **Move timeline** — ask why (scope change, dependency slip, resource constraint), identify downstream impacts on dependent items, flag anything moving past a hard deadline.
5. **Create new roadmap** — ask timeframe (quarter/half/year) and format preference (Now/Next/Later, quarterly themes, OKR-aligned, timeline/Gantt), gather the initiative list.

**Roadmap format frameworks (embedded):**
- **Now/Next/Later** (default, most teams most of the time): Now = committed, high confidence, actively building. Next (1-3 months) = planned, scoped, not yet started. Later (3-6+ months) = directional strategic bets, timing flexible. Best for external/leadership communication — avoids false precision.
- **Quarterly Themes:** 2-3 themes per quarter, each mapping to company/team OKRs, with initiatives listed under each. Good for showing strategic alignment.
- **OKR-Aligned:** initiatives listed under each Key Result they move, with expected impact. Creates accountability between what's built and what's measured.
- **Timeline/Gantt:** calendar-based, shows dependencies and parallelism. Good for engineering execution planning; NOT for external communication (creates false precision).

**Prioritization frameworks (embedded, use when reprioritizing):**
- **RICE** = (Reach × Impact × Confidence) / Effort. Reach = concrete number of users/customers affected per period. Impact = 3 (massive) to 0.25 (minimal). Confidence = 100% (data-backed) to 50% (gut feel). Effort = person-months. Best for a large, quantifiable backlog.
- **MoSCoW** — Must have (non-negotiable) / Should have (important, viable without) / Could have (lower priority, only if capacity allows) / Won't have (explicitly out of scope). Best for scoping a release and forcing prioritization conversations.
- **ICE** = Impact × Confidence × Ease (each 1-10). Simpler than RICE — good for early-stage products or thin data.
- **Value vs. Effort Matrix** — plot on a 2×2: Quick wins (high value/low effort, do first), Big bets (high value/high effort, scope carefully), Fill-ins (low value/low effort, spare capacity), Money pits (low value/high effort, don't do).

**Dependency handling (embedded):** categorize as technical, team, external, knowledge, or sequential. Always assign an owner and a "need by" date to each dependency; build buffer around them (they're the highest-risk items on any roadmap); flag cross-team dependencies early.

**Capacity allocation guideline (embedded):** a healthy default is 70% planned features / 20% technical health / 10% unplanned buffer — adjust for context (new product skews toward features, mature product toward tech debt, post-incident toward reliability). If commitments exceed capacity, cut scope — don't pretend the team can do more.

**Communicating changes (embedded):** acknowledge the change directly, explain what new information drove it, show the tradeoff (what got deprioritized or slipped), show the new plan, and acknowledge who's affected. Batch updates at natural cadences rather than reacting to every new data point — frequent roadmap changes often signal unclear strategy, not good responsiveness.

**Reasoning:**
- A roadmap is a communication tool, not a project plan — keep it at the right altitude (themes and outcomes, not tasks)
- Reprioritization should be driven by new information, not whim — always ask "what changed?"
- Dependencies are the single biggest risk to any roadmap — surface them explicitly, never bury them

**Skill source:** [roadmap-update](https://github.com/anthropics/knowledge-work-plugins/tree/main/product-management/skills/roadmap-update)

**Common mistakes:**
- Adding an item without asking what comes off (roadmaps are zero-sum against capacity)
- Reprioritizing without stating what new information drove the change
- Presenting a Gantt-style timeline externally (creates false precision and expectations)
- Not surfacing dependencies explicitly — they're the highest-risk items and get buried most often

---

### Card 14: Sprint Planning

**Trigger phrases:** "sprint planning", "plan the next sprint", "size this backlog against capacity", "what's P0 vs. stretch this sprint", "handle carryover"

**Core question it answers:** What can this team realistically commit to this sprint, and what's the plan if something slips?

**Required inputs:**
- Team and availability (who's on it, PTO/on-call/meetings this sprint)
- Sprint length (days/weeks)
- Backlog (prioritized list — pull from tracker, paste, or describe)
- Carryover from last sprint (anything unfinished)
- Cross-team dependencies (anything blocked on other teams)

**Interaction mode:** Document-shaped output — closest of the 5 operational skills to a fixed template. Produces a markdown table set (or the Part 2 HTML template if the user wants a polished version for sharing).

**Output template (embedded verbatim from the source skill):**

```markdown
## Sprint Plan: [Sprint Name]
**Dates:** [Start] — [End] | **Team:** [X] engineers
**Sprint Goal:** [One clear sentence about what success looks like]

### Capacity
| Person | Available Days | Allocation | Notes |
|--------|---------------|------------|-------|
| [Name] | [X] of [Y] | [X] points/hours | [PTO, on-call, etc.] |
| **Total** | **[X]** | **[X] points** | |

### Sprint Backlog
| Priority | Item | Estimate | Owner | Dependencies |
|----------|------|----------|-------|--------------|
| P0 | [Must ship] | [X] pts | [Person] | [None / Blocked by X] |
| P1 | [Should ship] | [X] pts | [Person] | [None] |
| P2 | [Stretch] | [X] pts | [Person] | [None] |

### Planned Capacity: [X] points | Sprint Load: [X] points ([X]% of capacity)

### Risks
| Risk | Impact | Mitigation |
|------|--------|------------|
| [Risk] | [What happens] | [What to do] |

### Definition of Done
- [ ] Code reviewed and merged
- [ ] Tests passing
- [ ] Documentation updated (if applicable)
- [ ] Product sign-off

### Key Dates
| Date | Event |
|------|-------|
| [Date] | Sprint start |
| [Date] | Mid-sprint check-in |
| [Date] | Sprint end / Demo |
| [Date] | Retro |
```

**Reasoning:**
- Sprint plans that ignore PTO/meetings/on-call systematically overcommit — capacity must be net of overhead, not headcount × days
- A sprint without one clearly-statable goal is unfocused — if you can't say it in one sentence, the scope isn't tight enough
- Honest carryover analysis (why didn't it ship?) prevents re-committing to the same failure mode

**Skill source:** [sprint-planning](https://github.com/anthropics/knowledge-work-plugins/tree/main/product-management/skills/sprint-planning)

**Tips (embedded):**
- **Leave buffer** — plan to 70-80% of nominal capacity; interrupts always happen
- **One clear sprint goal** — if it can't be stated in one sentence, the sprint isn't focused
- **Identify stretch items explicitly** — know in advance what gets cut if things run long
- **Carry over honestly** — understand *why* something didn't ship before re-committing to it this sprint

**Common mistakes:**
- Planning to 100% of nominal capacity (guarantees overcommitment the moment anything goes wrong)
- No single sprint goal — a list of unrelated tickets instead of a focused bet
- Silent re-commitment of carryover items without asking why they slipped
- P0/P1/P2 assigned without a real "would we not ship without this?" test on each P0

---

### Card 15: Stakeholder Update

**Trigger phrases:** "stakeholder update", "write a status update", "weekly/monthly update for leadership", "launch announcement", "escalate this risk", "translate this for [audience]"

**Core question it answers:** What does this specific audience need to know, and what do I need from them?

**Required inputs:**
- Update type: Weekly, Monthly, Launch, or Ad-hoc
- Audience: Executives/leadership, Engineering, Cross-functional partners, Customers/external, or Board
- What was accomplished since the last update
- Current blockers or risks
- Key decisions made or needed
- What's coming next

**Interaction mode:** Document-shaped output, but the shape depends entirely on audience — this card is a 5-audience × 4-type matrix, not one fixed template. Ask update type and audience first; everything else follows from that combination.

**Output templates by audience (embedded verbatim from the source skill):**

**Executive/leadership** — keep under 200-300 words, lead with the conclusion not the journey:
```
Status: [Green / Yellow / Red]
TL;DR: [One sentence — the most important thing to know]
Progress:
- [Outcome achieved, tied to goal/OKR]
Risks:
- [Risk]: [Mitigation plan]. [Ask if needed].
Decisions needed:
- [Decision]: [Options with recommendation]. Need by [date].
Next milestones:
- [Milestone] — [Date]
```

**Engineering** — link to tickets/PRs, explain the "why" behind priority changes:
```
Shipped:
- [Feature/fix] — [Link to PR/ticket]. [Impact if notable].
In progress:
- [Item] — [Owner]. [Expected completion]. [Blockers if any].
Decisions:
- [Decision made]: [Rationale]. [Link to ADR if exists].
Priority changes:
- [What changed and why]
Coming up:
- [Next items] — [Context on why these are next]
```

**Cross-functional partners** — what's coming that affects them, what you need from them, by when:
```
What's coming:
- [Feature/launch] — [Date]. [What this means for your team].
What we need from you:
- [Specific ask] — [Context]. By [date].
Decisions made:
- [Decision] — [How it affects your team].
Open for input:
- [Topic we'd love feedback on] — [How to provide it].
```

**Customers/external** — no internal jargon, frame everything as what the customer can now DO:
```
What's new:
- [Feature] — [Benefit in customer terms]. [How to use it / link].
Coming soon:
- [Feature] — [Expected timing]. [Why it matters to you].
Known issues:
- [Issue] — [Status]. [Workaround if available].
Feedback:
- [How to share feedback or request features]
```

**Status color framework (embedded):**
- **Green (On Track)** — use only when things are genuinely going well, not as a default
- **Yellow (At Risk)** — move here at the *first* sign of risk, not once you're sure it's bad; the earlier you flag, the more options you have
- **Red (Off Track)** — you've exhausted your own options and need escalation; don't wait until it's too late

**ROAM risk framework (embedded, for the Risks section of any audience):** Resolved / Owned (someone actively managing, state the plan) / Accepted (known risk, proceeding anyway, document why) / Mitigated (action taken, risk reduced to acceptable level).

**Reasoning:**
- Every audience gets a different altitude of the same underlying truth — executives get outcomes, engineers get implementation detail, customers get benefits with zero jargon
- Status colors must reflect genuine assessment, not what you think the audience wants to hear — Yellow is good risk management, not failure
- An "ask" must be specific and actionable ("decision on X by Friday," not "we need support")

**Skill source:** [stakeholder-update](https://github.com/anthropics/knowledge-work-plugins/tree/main/product-management/skills/stakeholder-update)

**Common mistakes:**
- Burying the lead — the most important thing (especially bad news) should come first, not after the good news
- Vague asks — "we need help" isn't an ask; "we need a decision on X by Friday" is
- Status color inflated to Green when it should already be Yellow — flagging risk early is a planning input, flagging it late is a fire drill
- Wrong altitude for the audience — technical implementation detail to executives, or vague strategic framing to engineers who need specifics

---

## Part 7: Delivery Skills

Two skills for validating and sizing delivery work before (and during) building the roadmap from Card 6. Both are directly invokable on their own, not just steps inside roadmap-building.

**Fuller worked examples for both skills below are in the companion file, `Product-Management-Assistant-Examples.md`.**

---

### Card 16: Epic Hypothesis

**Trigger phrases:** "frame this as an epic hypothesis", "is this epic validated", "what's our hypothesis for this initiative", "before we commit to the roadmap"

**Core question it answers:** What do we believe will happen if we build this, and how will we know if we're wrong — before we commit to building it?

**Required inputs:**
- The initiative or epic idea (a sentence is enough to start)
- Helpful if available: the target user/persona, the outcome expected, how it might be measured

**Interaction mode:** Component/fill-in-template output — short, structured, meant to precede Card 6 (MVP/Roadmap) or Card 17 (Epic Breakdown) work, not a long document on its own.

**This is not a requirements spec — it's a hypothesis being tested, not a feature being committed to shipping.**

**Structure (embedded, from Tim Herbig's Lean UX hypothesis format):**

```markdown
### If/Then Hypothesis
**If we** [action or solution on behalf of the target persona]
**for** [target persona]
**Then we will** [attain or achieve a desirable outcome or job-to-be-done]

### Tiny Acts of Discovery Experiments
**We will test our assumption by:**
- [Experiment 1]
- [Experiment 2]

### Validation Measures
**We know our hypothesis is valid if within** [timeframe]
**we observe:**
- [Quantitative measurable outcome]
- [Qualitative measurable outcome]
```

**Quality checks per section:**
- **"If we" is specific:** not "improve the product" but "add one-click Slack notifications when tasks are assigned"
- **"For" is a clear persona:** not "users" but "remote project managers juggling 3+ distributed teams"
- **"Then we will" is an outcome, not an output:** not "users will have notifications" but "users will respond to task assignments 50% faster"
- **Experiments are fast and cheap:** days/weeks, not months; prototypes and manual processes, not full engineering builds
- **Validation measures are specific and falsifiable:** not "users are happy" but "80% of surveyed users rate the feature 4+ of 5"; not "within 6 months" but a 2-4 week validation cycle

**Experiment types to suggest:** prototype + user testing (clickable prototype, 5-10 users), concierge test (manually perform the feature for a few users), landing page test (describe the feature, measure signups/interest), Wizard of Oz test (present as automated, do it manually behind the scenes), lightweight A/B test.

**Good/bad examples (embedded):**
- ✅ "If we add one-click Google Calendar integration for trial users, then we will increase activation rates by 20% within 30 days"
- ❌ "If we build a dashboard, then users will use it" (vague, not measurable, describes output not outcome)

**Anti-patterns (what this is NOT):**
- Not a feature spec — "build a dashboard with 5 charts" is a feature, not a hypothesis
- Not a guaranteed commitment — hypotheses can and should be invalidated
- Not output-focused — "ship feature X by Q2" misses whether it achieved the outcome
- Not experiment-free — skipping straight to full build means you're not testing anything

**Common pitfalls:**
1. **Hypothesis is a feature, not an outcome** — "if we build a dashboard, we'll have a dashboard." Fix: state the user outcome the dashboard produces.
2. **Skipping experiments** — "we'll test our assumption by building the full feature." Fix: design a lightweight prototype/concierge/landing-page test that takes days, not months.
3. **Vague validation measures** — "we know it's valid if users are happy." Fix: define specific, falsifiable metrics.
4. **Unrealistic timeframes** — "valid if within 6 months revenue increases" is too slow to inform any decision. Fix: 2-4 week validation cycles, using a leading indicator if the ultimate metric is too slow.
5. **Treating epics as commitments** — "we already told the CEO we're shipping this." Fix: frame epics as hypotheses *before* making commitments to stakeholders.

**Reasoning:**
- Hypothesis-driven framing forces the team to state what they believe (and could be wrong about) before spending months building it
- "Then we will" keeps the focus on user/business outcome, not on the feature being shipped
- Falsifiable success criteria make it possible to kill a bad idea early, cheaply — the entire point of the format

**Skill source:** [epic-hypothesis](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/epic-hypothesis)

**Ties back to:** Card 6 (MVP/Roadmap Proposal) uses this as its Section 1 ("01 Epic Hypothesis"). Once a hypothesis is validated, decompose it into user stories — if the resulting story is still too large to estimate or sequence safely, hand it to Card 17 (Epic Breakdown Advisor).

---

### Card 17: Epic Breakdown Advisor

**Trigger phrases:** "break this epic down", "this backlog item is too big", "split this into stories", "which splitting pattern should I use", "size this for a sprint"

**Core question it answers:** How do we split this epic into stories that each deliver real user value, without slicing it into meaningless technical layers?

**Required inputs:**
- The epic or large story to break down (paste as written in the backlog)
- Helpful if available: team context (sprint length, estimation ceiling), what's blocking delivery (too big to estimate, sequence, or release)

**Interaction mode:** Interactive, sequential — walk the epic through a fixed flowchart one question at a time rather than dumping the whole framework and asking the user to self-serve. This mirrors the source skill's own interactive design; don't skip steps to save time.

**Step 1 — Pre-Split Validation (INVEST check, except "Small"):** ask sequentially:
1. **Independent?** Can this be prioritized/developed without hard technical dependencies on other stories?
2. **Negotiable?** Does it leave room for the team to discover implementation details, or is it over-prescribed?
3. **Valuable?** Does it deliver observable value to a user? **⚠️ Critical stop:** if this fails, don't split — it's a technical task, not a user story. Combine it with related work instead.
4. **Estimable?** Can the team size it relatively, even roughly?
5. **Testable?** Does it have concrete, verifiable acceptance criteria?

If it passes all checks (or "Valuable" is the only one truly gating), proceed to Step 2. If any other check fails, fix that issue before splitting.

**Step 2 — Apply the 9 splitting patterns, in this order, stopping at the first that fits:**

1. **Workflow Steps** — split into thin end-to-end slices (full workflow, increasing sophistication), never step-by-step layers. Trigger question: "Does this involve a multi-step workflow where a simple full-path case could ship first?"
2. **Operations (CRUD)** — words like "manage," "handle," "maintain" signal bundled operations. Trigger question: "Does this bundle Create/Read/Update/Delete style operations?"
3. **Business Rule Variations** — different rules for different scenarios (user types, regions, tiers) become separate stories. Trigger question: "Are there different business rules for different scenarios here?"
4. **Data Variations** — different data types/structures, added just-in-time. Trigger question: "Does this handle different data types or structures?"
5. **Data Entry Methods** — ship the simplest UI first, fancy UI (date pickers, drag-and-drop) as a follow-up. Trigger question: "Are there UI elements here that aren't essential to core functionality?"
6. **Major Effort** — first implementation is hard, additional variants are trivial ("implement one + add remaining"). Trigger question: "Is there infrastructure here where the first build is hard but more variants are easy?"
7. **Simple/Complex** — identify the simplest version that still delivers value, extract variations as follow-ups. Trigger question: "What's the simplest version of this that still delivers value?"
8. **Defer Performance** — split "make it work" from "make it fast" (performance/security/scale can follow functional delivery). Trigger question: "Can functional value ship first, with optimization as a follow-up?"
9. **Break Out a Spike** (last resort) — when uncertainty itself prevents splitting, time-box a 1-2 day investigation to answer the specific unknown, then restart at Pattern 1 with better information. Not a shippable story — it produces learning.

**Meta-pattern applied across all 9:** identify the core complexity → list all variations → reduce to one complete slice → make the rest separate stories.

**Step 3 — Evaluate the split.** After splitting, check:
- Does this split reveal low-value work that can be deprioritized or eliminated? (Good splits expose the 80/20 — most value concentrates in a small slice.)
- Does this split produce roughly equal-sized stories? (Gives the Product Owner more prioritization flexibility.)

If neither holds, try a different pattern.

**Cynefin domain check (embedded, informs how exhaustively to split):**
- **Low uncertainty (Obvious/Complicated):** find all stories, prioritize by value/risk
- **High uncertainty (Complex):** identify 1-2 learning stories only; avoid exhaustive enumeration — the work itself teaches what matters
- **Chaos:** defer splitting entirely until stability emerges; focus on stabilization first

**Output template (embedded):**

```markdown
# Epic Breakdown Plan
**Epic:** [Original epic]
**Pre-Split Validation:** ✅ Passes INVEST (except Small)
**Splitting Pattern Applied:** [Pattern name]
**Rationale:** [Why this pattern fits]

## Story Breakdown
### Story 1: [Title] (Simplest Complete Slice)
**Use Case:** As a [persona], I want to [action] so that [outcome]
**Acceptance Criteria:** Given [preconditions], When [action], Then [outcome]
**Why This First:** [delivers core value; simpler variations follow]
**Estimated Effort:** [days/points]

### Story 2, 3...: [repeat]

## Split Evaluation
✅ Does this split reveal low-value work? [analysis]
✅ Does this split produce equal-sized stories? [analysis]

## INVEST Validation (Each Story)
[Confirm each story independently passes INVEST]

## Next Steps
1. Review with team
2. Check for further splitting (>5 days? restart at Pattern 1 for that story)
3. Prioritize
4. Consider eliminating low-value stories the split revealed
```

**Reasoning:**
- Vertical slices (full workflow, thin) preserve user value; horizontal slices (front-end story, back-end story) preserve nothing — neither delivers observable behavior on its own
- Working through 9 patterns *in order* prevents arbitrary, guessed splits — the sequence itself is the discipline
- A split that doesn't reveal low-value work or produce more equal-sized stories isn't actually a good split — it's just smaller pieces of the same problem

**Skill source:** [epic-breakdown-advisor](https://github.com/deanpeters/Product-Manager-Skills/tree/main/skills/epic-breakdown-advisor)

**Common pitfalls:**
1. **Skipping pre-split validation** — splitting a story that isn't even Valuable (it's a technical task in disguise)
2. **Step-by-step workflow splitting done wrong** — "Story 1: editorial review, Story 2: legal approval" delivers nothing until the last story ships. Fix: each story covers the *full* workflow, just with increasing sophistication.
3. **Horizontal slicing** — "Story 1: build API, Story 2: build UI" — neither delivers user value alone. Fix: vertical slices only.
4. **Forcing a pattern that doesn't fit** — if the trigger question is genuinely "no," say no and move to the next pattern, don't force it.
5. **Not re-splitting large stories** — if a resulting story is still 5+ days, restart at Pattern 1 for that story specifically.
6. **Skipping the split evaluation step** — splitting without asking whether it revealed low-value work wastes the exercise's biggest benefit.

**Ties back to:** Card 6 (MVP/Roadmap Proposal) — use this when Phase 1's scope, once hypothesis-validated via Card 16, is still too large to estimate, sequence, or ship safely as one story.

---

## Quick Reference: When to Use Each Skill

| Situation | Skill(s) to Use | Order |
|---|---|---|
| Quarterly business review | Cards 2, 10 | Health check first, then strategic asks |
| Pitching a new product line | Cards 1, 3, 4, 5, 10 | Build evidence (1-5), then ask (10) |
| Engineering scoping meeting | Cards 6, 7, 8 | Roadmap, spec, feasibility |
| Board meeting prep | Cards 2, 4, 5, 10 | Health + strategy + decision |
| Competitive threat response | Cards 3, 4, 5, 10 | Understand market + reposition + ask |
| Post-launch review | Card 2 (update) + Card 10 | New health baseline, lessons learned |
| Weekly team check-in | Card 11 (light) or Card 15 (Engineering audience) | Whichever cadence the team runs |
| Sprint kickoff | Card 16 (if new epic) → Card 17 (if too big) → Card 14 | Validate, size, then plan the sprint |
| Backlog item too big to estimate | Card 17 | Standalone — walk the 9 patterns |
| Need to think through a fuzzy problem | Card 12 | Standalone, can precede Card 1 |
| Roadmap needs to change | Card 13 | Standalone, references existing roadmap |
| Monthly stakeholder or exec update | Card 15 (Executive audience) | Standalone, or after Card 11 |

**Humanizing is orthogonal to which skill you pick** — the humanizer flag (Part 3.6) can be added to any document-shaped output in the table above. It's a style pass, not a skill of its own, and it stays off unless explicitly requested.

---

**End of Knowledge Base.**

Next steps: Copy this entire document, paste into ChatGPT-5 (upload `Product-Management-Assistant-Examples.md` alongside it for fuller worked examples of Cards 11-17), then name a document type or skill and provide your inputs. Add the humanizer flag (Part 3.6) to any request if you want the output rewritten to sound less AI-generated.
