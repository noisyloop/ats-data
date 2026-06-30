# Roadmap: An Open-Source ATS Built to Fix What's Documented to Be Broken

*A build roadmap, not a finished spec. Every design decision below is traceable to a specific documented problem from "2026 Job Reality of ATS — Complete Reference." This isn't a generic "fair hiring" wishlist — it's a direct response to the failure modes the research actually found.*

---

## Why This Exists

Every major ATS reviewed in this research — Workday, Greenhouse, Lever, the third-party layers like HireVue and Pymetrics — shares the same structural pattern: black-box scoring, opt-in (not default) fairness features, AI recommendations shown to humans without safeguards, and bias-audit compliance treated as a bolt-on for regulators rather than a built-in product feature. None of that is a law of nature. It's a set of choices, and they're choices an open-source project can make differently from day one.

---

## The Holes — What's Actually Documented to Be Broken

This table is the core of the roadmap. Every row is a specific, sourced finding; every fix is a concrete design decision, not an aspiration.

| # | Documented Problem | Evidence | This Roadmap's Fix | Phase |
|---|---|---|---|---|
| 1 | Resume parsing scrambles non-standard formatting, penalizing qualified applicants for formatting choices, not content | ATS parsing internals (OCR/NLP left-to-right extraction) | Structured-input-first design — candidates fill structured fields directly; PDF upload is supplementary, never authoritative | 1 |
| 2 | TF-IDF scoring penalizes legitimate keyword repetition as "stuffing" | TF-IDF matching mechanics | Don't ship TF-IDF as a default scoring path; if offered, document and bias-test it explicitly before enabling | 3 |
| 3 | Semantic/embedding matching inherits racial and gender bias from the underlying model | Wilson & Caliskan (2024): 85% white-male favorability, 0% Black-male-vs-white-male favorability across 3 real embedding models | Never feed name or other PII into the matching step; pluggable scoring backends must publish a model card with bias-audit results before they can be registered | 3 |
| 4 | Recruiters and candidates never see the match score or its reasoning | ATS scoring internals (black-box dashboard) | Rubric weights are visible to candidates, not hidden; score breakdown is a first-class UI element, not a backend-only number | 3 |
| 5 | Knockout questions are blunt, undocumented, and function as informal national-origin proxies | Knockout question mechanics; SiriusXM case (education/address as race proxy) | Knockout questions must cite a specific legal basis from a defined enum (visa category, license type, etc.) — no open-ended "are you authorized to work" with no further structure | 1 |
| 6 | Most applications are never actually reached by a human, due to volume, not rejection — and applicants have no visibility into which happened | The corrected "three-bucket" finding: knockouts vs. content auto-reject vs. simply never reached | Explicit status taxonomy visible to candidates: Submitted → Under Review → Knockout Failed (reason shown) → Reviewed, Not Selected → Not Yet Reached. "Not yet reached" is a real, honest state, not hidden behind silence | 1, 7 |
| 7 | Proxy variables (zip code, university name, employment gaps) drive bias without any explicit race/age/disability field | Proxy-variable mechanism; Mobley v. Workday's core theory | Blind review is the **default**, not opt-in: name, photo, university, zip/address auto-redacted from the recruiter view. Override requires an explicit, logged reason | 2 |
| 8 | Blind/redacted hiring already exists in commercial ATS platforms but is opt-in and rarely enabled | Documented in "things applicants aren't told" | Same fix as #7 — flip the default | 2 |
| 9 | Showing a human a biased AI recommendation shifts the human's own decision to match it, even with the human nominally in control | UW Nov 2025 study: human selections mirrored AI bias rates even at "moderate," real-world-calibrated levels | Independent-judgment-first workflow: recruiter must submit their own assessment before any AI-generated recommendation is revealed. The AI panel is UI-locked until then | 4 |
| 10 | LLM evaluation outcomes shift based on resume presentation order, independent of content | Puutio & Lin (2025): positional bias in simulated ChatGPT screening | Randomize/rotate candidate presentation order per recruiter session; no model or recruiter ever sees a fixed submission-order list | 4 |
| 11 | Bias-audit compliance (NYC Local Law 144, EU AI Act) is reactive — companies audit after deployment, if at all | Regulatory landscape section | Continuous, built-in aggregate bias dashboard from day one — disparate-impact flagging and an auto-generated, publishable audit report are core features, not a compliance add-on | 5 |
| 12 | EEO self-identification data is "supposed to be" siloed from hiring decisions but lives in the same system as everything else | EEOC self-ID procedural-vs-practical gap | Real architectural separation: EEO data lives in a separate service/store with no foreign key reachable by any recruiter-facing role. Aggregate-only joins for the bias dashboard (#11), never per-record | 0, 5 |
| 13 | Ghost job postings stay open with no real hiring intent, wasting applicant effort | "Things applicants aren't told" — ghost jobs | Postings require a review-by/expiration date at creation; auto-flag as "may be paused" after N days with zero recruiter activity, visible to applicants | 1, 7 |
| 14 | ID/biometric verification is increasingly collected upfront, before any payout or offer, with documented refusal to delete on request elsewhere in this research (the gig-platform side of this project) | Outlier/Mercor research from earlier in this project | Tiered verification: nothing required to apply; identity checks escalate only at offer stage, never before compensation exists | 6 |
| 15 | Disability gets penalized indirectly through gap-detection and gamified/video assessments | Disability bias section (Pymetrics, HireVue criticism) | No gamified or video-based assessment in the default product; if added later, requires its own bias audit before activation, same standard as #3 | 3, 5 |
| 16 | Candidates get no explanation when filtered, just silence | "Talent Network black hole" finding | Right-to-explanation is automatic: candidates can see exactly which knockout or rubric category excluded them, not just a generic rejection or no response at all | 7 |
| 17 | Real-time deepfake/synthetic identity fraud in remote hiring is a genuine, growing threat, not just a justification for invasive ID collection | DPRK hiring fraud research (Unit 42, DOJ, FBI data) | Verification proportionate to actual risk: optional liveness checks for roles/orgs that opt into an elevated-risk tier, disclosed to the candidate why, not a blanket default | 6 |

---

## Design Principles

These aren't separate from the table above — they're the pattern underneath all of it:

1. **Transparency by default, not by request.** If a feature reduces bias or increases honesty, it ships on, and the recruiter has to actively choose to turn it off (and that choice is logged).
2. **Honest status over silence.** "Not yet reached" is a real, displayable state. Every other ATS in this research effectively hides that bucket behind generic rejection or no response at all.
3. **No scoring system without a model card.** Any pluggable matching backend has to publish what it's tested on and what bias it carries, the same standard this whole research project has applied to every claim in it.
4. **Compliance is a feature, not a chore.** NYC LL144 and EU AI Act-style audits should be something the product generates automatically, not something a company scrambles to commission after the fact.

---

## Phased Build Plan

### Phase 0 — Architecture Foundations
- Core entities: `Candidate`, `Application`, `Posting`, `Rubric`, `KnockoutQuestion`, `AuditLog`
- Hard architectural separation between the EEO self-ID store and the candidate-scoring store — different service, no joinable foreign key for any recruiter-facing role (#12)
- Append-only, hash-chained audit log for every status change and override action — same pattern as immutable audit logging used elsewhere in your own security tooling, applied here to hiring decisions instead of system events
- Stack-agnostic spec, but worth noting: Cloudflare Workers + D1 would map cleanly onto this if you want to reuse infrastructure patterns you already have in production elsewhere

### Phase 1 — Minimal Viable ATS (Transparency-First)
- Structured-input-first application form (#1)
- Posting creation requires expiration/review-by date (#13)
- Knockout questions limited to a defined, legally-justified enum (#5)
- Candidate-visible status taxonomy including "Not Yet Reached" as a real state (#6, #16)

### Phase 2 — Blind Review by Default
- Auto-redaction of name, photo, university, zip/address in the recruiter view (#7, #8)
- Override requires explicit, logged justification
- Normalized experience/skill fields to reduce gap-visibility bias, with an optional candidate-controlled free-text context field

### Phase 3 — Fair Matching Engine
- Pluggable scoring backends, each requiring a published model card and bias-audit result before registration (#3, #15)
- No PII fed into any embedding/matching step
- Visible rubric weights, not a hidden score (#4)
- No default TF-IDF keyword-density penalty without explicit testing (#2)

### Phase 4 — Human-AI Interaction Safeguards
- Independent-judgment-first workflow: recruiter score locked in before any AI recommendation is shown (#9)
- If AI output is shown at all, no per-candidate numeric score — qualitative reasoning only, to reduce anchoring
- Randomized/rotated presentation order to counter positional bias (#10)

### Phase 5 — Built-In Continuous Bias Auditing
- Aggregate-only demographic outcome dashboard, joined from the separated EEO store at the statistical level only (#11, #12)
- Automatic disparate-impact flagging (e.g., four-fifths rule) per posting, role, and recruiter
- Auto-generated, publishable audit report in a NYC LL144-compatible format

### Phase 6 — Risk-Proportionate Identity Verification
- No verification required to apply; escalates only at offer stage, never before any compensation exists (#14)
- Optional liveness/ID checks gated behind an explicit elevated-risk tier, disclosed to candidates (#17)
- Optional portfolio/contribution-based signal module for technical roles (the GitHub-only concept from earlier in this project) as one input among several — never the sole gate

### Phase 7 — Applicant-Facing Transparency Tools
- Real-time status and queue visibility, including recruiter review-coverage stats
- Posting health indicators (age, applicant count, "may be paused" auto-flag)
- Automatic right-to-explanation for any exclusion (#16)

### Phase 8 — Open-Source Governance
- Public model cards for every matching backend, published bias-audit results regardless of outcome
- RFC-style process for any change to rubric or scoring logic
- Independent third-party audit cadence, with results published whether favorable or not
- Plugin architecture so other orgs/auditors can swap and independently test matching models

---

## Open Questions to Resolve Before Building

- **License:** Apache 2.0 would be consistent with how you've licensed loopwatch — worth deciding early since it affects how comfortable enterprise adopters are contributing back.
- **Deployment model:** self-hosted single-tenant per company, or a multi-tenant hosted option? This affects how strictly the EEO-data architectural separation (#12) needs to be enforced at the infrastructure level versus the application level.
- **Scope of v1:** the full table above is a lot of surface area. Worth picking 3-4 rows as the actual MVP differentiators rather than trying to ship all 17 holes at once — the blind-review default (#7/#8) and honest status taxonomy (#6/#16) are probably the highest-leverage, lowest-effort starting point.
