# 2026 Job Reality of ATS — Complete Reference

*A comprehensive, merged reference compiled mid-2026 from court filings, EEOC and OMB guidance, peer-reviewed and preprint research, recruiter surveys, and security research. Combines and expands on all prior sections into a single document. Not legal advice. Litigation status, regulatory deadlines, and recruiter practices are subject to change — verify current status before relying on any specific legal claim below.*

---

## Table of Contents

- Part I — How ATS Systems Actually Work
- Part II — Does a Human Ever Actually See Your Resume?
- Part III — Documented Bias
- Part IV — The Legal and Regulatory Landscape
- Part V — The Other Side of Verification: Synthetic Identity Fraud
- Part VI — What Applicants Generally Aren't Told
- Sources Referenced

---

# PART I — How ATS Systems Actually Work

## 1. How Parsing Actually Works

An ATS does not "read" a resume the way a human does. When you upload a PDF or Word document, the system runs Optical Character Recognition (OCR) and Natural Language Processing (NLP) to extract text and sort it into structured fields: name, contact info, work history, education, skills.

The common failure mode here is formatting, not content. Parsers generally read left-to-right, top-to-bottom. Complex columns, tables, graphics, or unusual fonts can scramble the extraction, producing a garbled or incomplete record that's effectively unrankable, regardless of how qualified the candidate actually is. This is a structural limitation of the parsing technology, not a judgment about the applicant.

## 2. Keyword Matching Algorithms

Once parsed, your structured data gets compared against the job requisition. Three approaches are in active use, often layered together depending on how old or modern the platform is:

- **Exact Match (Boolean):** A strict query like ("Python" OR "Java") AND ("AWS" OR "Azure"). If the exact string wasn't parsed correctly, it doesn't count, regardless of whether you actually have the skill.
- **TF-IDF (Term Frequency-Inverse Document Frequency):** Older systems count how often a keyword appears in your resume relative to how common that word is across all resumes. Repeating "Python" excessively can actually lower its weight, since the system interprets the repetition as keyword-stuffing rather than depth of experience — a counterintuitive failure mode for anyone trying to "beat the system" by cramming keywords in.
- **Semantic Search (Vector/Embedding Matching):** Modern systems map both the resume and job description into a shared vector space. If the posting asks for "B2B Sales" and your resume says "Enterprise Account Executive," the system can recognize semantic closeness and credit it, even without an exact keyword match. This is also the technology layer where the racial and gender bias findings in Part III become most directly relevant, since embedding models trained on biased data carry that bias into the matching step itself.

## 3. Scoring and Ranking

Most systems generate a numeric Match Score, often expressed as 0-100%. How that score gets used varies by employer:

- **Knockout Questions:** Binary eligibility checks set by a human recruiter, not the algorithm: work authorization status, an active required license, a minimum years-of-experience threshold. Fail one, and you're typically filtered out regardless of your overall score. These are described in the industry as "legally defensible" rejections because they're applied uniformly to every applicant rather than being a content judgment.
- **Weighted Keywords:** Recruiters can assign point values: a required skill might be worth 10 points, a preferred skill 5, years of experience up to 20.
- **Recruiter Dashboard:** Candidates are typically displayed sorted by score, highest first, with the recruiter working down the list until they've found enough qualified candidates or run out of time.

## 4. What Data ATS Platforms Actually Collect

Far more than the resume itself:

- Parsed resume fields (name, contact info, work history, education, skills)
- The application form itself, often duplicating resume data plus custom screening questions
- Cover letter text
- Assessment or test scores, if the role requires one
- Source tracking (which job board, referral, or link brought you there)
- Behavioral metadata: time spent on the form, which fields were edited, IP address, device fingerprint
- Video interview recordings and transcripts, where that stage is used
- A voluntary EEO self-identification survey (see Part III, Section 20)

## 5. Other Filtering Attributes

Beyond keyword matching, several metadata-driven filters shape who gets seen:

- **Source Tracking:** The system tracks where an applicant came from (LinkedIn, Indeed, employee referral, company site). Referrals are frequently surfaced to the top of the queue, since internal data often shows referrals have higher retention rates — meaning two identical resumes can get very different treatment purely based on how they entered the pipeline.
- **Recency Filtering:** If a job has been open 30 days with 500 applicants, a recruiter may filter to view only submissions from the last 48 hours to find "fresh" candidates — meaning the timing of your application can matter as much as its content.
- **Structured Tagging:** Recruiters can manually tag candidates internally (e.g., "Silver Medalist" — good but not hired, "High Potential"). If you apply again later, the recruiter may see this tag from a previous cycle, for better or worse.

## 6. The Role of AI in Modern ATS

- **Workday** uses machine learning for "Suggested Candidates," surfacing applicants who match the profile of the company's past successful hires — the exact mechanism at the center of the litigation covered in Part IV.
- **Greenhouse and Lever** have historically been more recruiter-centric but now integrate with third-party AI tools (such as BrightHire or HireVue) layered on top of the core platform.
- **AI resume screeners** in some deployments generate a written recommendation directly, e.g., "Candidate has 6 years of retail experience but lacks B2B SaaS experience. Recommend: do not advance."
- **Interview intelligence** tools record video interviews, transcribe them, and analyze the transcript for "competencies" and "red flags," feeding that analysis back into the ATS record for future reference.

---

# PART II — Does a Human Ever Actually See Your Resume?

## 7. The "75% Rejected by Robots" Claim — Debunked, But Not Replaced With Its Opposite

A widely circulated statistic claims that 75% of resumes are rejected by ATS software before a human ever sees them. This number traces back to a single 2012 sales pitch from a company called Preptel, which went out of business in August 2013. No research methodology was ever published, and no study has reproduced the figure.

What better-sourced data shows:

- A 2025 Enhancv interview study of 25 US recruiters across tech, healthcare, and finance found only 8% configure any content-based auto-rejection at all. Knockout questions (eligibility checks, not content scoring) are used by effectively 100% of recruiters, but those are narrow, employer-defined filters, not a black-box rejection engine.
- Harvard Business School's 2021 "Hidden Workers" study is frequently misquoted as proof of silent algorithmic rejection. What it actually found: more than 90% of companies use technology to rank and filter candidates, and technology may screen out qualified applicants in 88% of companies — but because of how searches and filters are configured by people, not because software autonomously deletes resumes.

**Correction worth flagging directly:** a frequently repeated counter-claim — that "90-95% of applications are reviewed by a human" (attributed to recruiter Jan Tegze) — is itself just one practitioner's personal estimate with no published methodology, the same evidentiary weight as the 75% myth it's used to rebut, not stronger evidence. It also directly contradicts other findings from the same body of recruiter-survey data: respondents report pausing review after roughly 300-500 strong applications even while a listing stays open, and that late applicants frequently arrive "after interviews have begun." If a posting draws 2,000 applicants and active review effectively stops once the recruiter has enough candidates from the first few hundred, the remaining 1,500+ were not auto-rejected by any algorithm — but they were also never opened by a human. Calling that "reviewed" is not accurate.

**The honest picture has three buckets, not two:** a small number of applications are filtered by explicit knockout questions (work authorization, license, experience minimum); a small number get killed by content-based auto-reject (roughly 8% of employers use this); and a large, unmeasured share simply sit unopened in a sorted queue once the recruiter stops actively reviewing — neither rejected nor reviewed, just never reached. That third bucket is the real volume bottleneck, and it's a hard ceiling, not a delay before eventual review.

This matters because it relocates where bias actually has teeth: not in a mythical instant auto-reject, but in whatever determines your position in that sorted queue — which is exactly where the active litigation in Part IV is focused.

## 8. The Competing 75%/25% Claim, As Commonly Cited Elsewhere

This claim resurfaces constantly, including via Google's AI Overview, so it's documented here directly rather than dismissed:

- "Up to 75% of resumes never make it past the automated ATS to a human recruiter's desk."
- "Among large companies, up to 98% use this software to scan and filter applications."
- "25% or less of all submitted resumes successfully pass the initial ATS filter to a recruiter's inbox."
- "No magic 'pass score': human recruiters never see the numeric match score directly — it's a backend sorting tool."
- "Very few systems automatically and permanently delete resumes without human oversight, but an unoptimized resume is easily invisible when recruiters search by keyword."

As cited elsewhere: IntelligentCV.app and KickResume.com (both ATS resume-optimization products), a Citizens Bank careers page, and two Reddit posts (r/jobhunting "analyzed 1.7M applications," r/jobsearchhacks "spent 8 months testing ATS systems") cited without visible published methodology.

**Source quality note, applied evenly:** the two product sites have a direct commercial incentive to keep this statistic alive, since their business is selling the fix to it — worth knowing, not disqualifying on its own. The Reddit posts may well be accurate but, as linked, carry the same evidentiary weight as the single-recruiter Tegze estimate corrected above: a claim, not a published study. By contrast, the Enhancv and Harvard Business School research cited above have visible methodology behind them. That doesn't make the 75% figure false — it means it currently has weaker sourcing than the competing data in this document, and both should be held to the same bar.

**Where the two pictures may actually converge:** the contested part isn't necessarily the outcome — both bodies of evidence agree a large share of resumes never reach a human. What's contested is the mechanism. One framing says the ATS algorithm itself is doing the filtering (implying keyword/formatting optimization is the fix). The other says it's mostly recruiter time and volume, with explicit algorithmic auto-reject being rare (implying timing, referrals, and avoiding parsing failures matter more than keyword density).

## 9. Practical Takeaways That Hold Under Either Explanation

- **Mirror the job description:** use the exact terms, phrases, and technical skills listed in the posting.
- **Avoid complex formatting:** no columns, tables, graphics, photos, or text boxes — a single-column, standard-heading format parses reliably under both TF-IDF and semantic matching.
- **Use standard job titles:** "Software Engineer," not a creative internal title, so the system categorizes your experience correctly.
- **Submit as .docx or .pdf:** avoid image-based files or design-exported PDFs that can't be text-parsed.
- **Apply early and use referrals where possible:** under the volume-bottleneck explanation, these matter more than keyword density.

---

# PART III — Documented Bias

## 10. The Pre-AI Baseline: Bertrand & Mullainathan (2004)

Racial bias in hiring predates AI by decades, and matters as a baseline because it establishes that the underlying discrimination didn't originate with algorithms — algorithms inherited it.

The foundational study here is **Bertrand & Mullainathan (2004)**, "Are Emily and Greg More Employable Than Lakisha and Jamal?" Researchers sent out thousands of otherwise-identical resumes to help-wanted ads in Boston and Chicago, varying only the applicant's name to signal race. Resumes with "white-sounding" names (Emily, Greg) received roughly **50% more callbacks** than identical resumes with "Black-sounding" names (Lakisha, Jamal) — equivalent to needing about 10 resumes sent to get one callback versus 15. On average, applicants with Black-sounding names needed roughly 8 additional years of experience to achieve the same callback rate as their white-named counterparts, and the gap actually widened as resume quality improved. No AI, no ATS — entirely human reviewers. This result has been replicated in various forms in the two decades since (Cotton et al. 2008; Kline et al. 2022; Nunley et al. 2015; Goldstein & Stecklov 2016).

Notably, this study explicitly excluded Hispanic- and Asian-associated names from its design — see Section 18 for why that matters for the literature that followed.

A larger, more recent replication (Kline, Rose & Walters, UC Berkeley and University of Chicago) sent 83,000 job applications to 108 Fortune 500 employers, finding applicants with Black names were called back 10% fewer times across the board, with the top 20% most discriminatory firms responsible for fully half of all callbacks lost to discrimination — indicating the problem is concentrated rather than evenly distributed across employers.

## 11. How Bias Enters Algorithmic Systems Without an Explicit Race Field

Even when an ATS or AI model never directly parses a race field, several proxies carry the same signal:

- **Names** — parsed directly from the resume and a strong demographic signal on their own.
- **Zip codes** — correlate with race and socioeconomic status due to historical housing segregation patterns.
- **University names** — a degree from a given institution can correlate with income, generational wealth, and (via institutions like HBCUs) race directly.
- **Employment gaps and "non-traditional" career paths** — disproportionately affect candidates from lower-income backgrounds and communities with less access to uninterrupted career tracks, and also function as a disability proxy (see Section 13).

## 12. Algorithmic Bias From Historical Training Data

If a company historically hired a narrow demographic profile for a given role and then enables an AI "recommended candidates" feature, the model learns that profile as the definition of a good hire. It can then down-rank candidates from HBCUs or women's colleges, or those with non-traditional career paths, not through any explicit rule, but because the training data encodes the company's past pattern. This is the central mechanism alleged in Mobley v. Workday (Part IV).

## 13. Disability Bias

- **Resume gaps:** People with chronic illness or disability histories often have employment gaps. ATS ranking algorithms frequently penalize gaps by assuming a lack of "recent relevant experience."
- **Formatting requirements:** Applicants with cognitive disabilities or dyslexia may use non-standard formats or struggle with complex application portals; parsers can reject or mangle anything non-standard, regardless of qualification.
- **Gamified assessments:** Tools like Pymetrics or HireVue have used neurological games or video-response analysis. These have been criticized for penalizing neurodivergent candidates (autism, ADHD) and candidates with motor-skill impairments, and for video-analysis AI failing to accurately read facial expressions across different disabilities and cultural backgrounds.

## 14. Age Bias

- Algorithms can screen out candidates with "too much" experience, sometimes as a proxy for higher expected salary.
- Mentioning older technologies by name (e.g., legacy mainframe systems, "Windows 95") can function as an inadvertent age signal.
- Filters set for "early career" based on graduation year automatically exclude older applicants regardless of fit.

## 15. What Recent Peer-Reviewed Research Found in LLM-Based Resume Screening

This is the most directly relevant recent evidence, since LLM-based screening is now in active commercial use.

**Wilson & Caliskan (2024), "Gender, Race, and Intersectional Bias in Resume Screening via Language Model Retrieval"** — presented at the AAAI/ACM Conference on AI, Ethics, and Society (AIES 2024), and separately summarized by the Brookings Institution. Researchers tested three high-performing text-embedding models (the kind used in real semantic resume-matching systems described in Section 2) against 554 real resumes and 571 real job descriptions across nine occupations.

Findings:

- White-male-associated names were favored by the models **85% of the time**.
- Female-associated names were favored only **11% of the time**.
- In direct pairwise comparisons, **Black-male-associated names were favored 0% of the time** against white-male-associated names, and only **14.8%** of the time against Black-female-associated names.
- Across 27 discrimination tests spanning three models and nine occupations, men's and women's names were selected at equal rates in only 37% of cases.
- The bias compounded at the intersection of race and gender — Black men were disadvantaged most severely of any group tested.

Related work (Puutio & Lin, 2025) ran 2,000 simulated applications through ChatGPT and found additional bias vectors beyond names: a preference for "elite" educational credentials, and **positional bias** — where a candidate's resume appears in the response order can itself influence the outcome, independent of content.

## 16. AI Bias Transfers to Human Decision-Makers

A November 2025 University of Washington follow-up study addressed a different question: does showing a human a biased AI recommendation change what the human decides, even though the human retains final say?

Researchers simulated resume screening where participants picked candidates to interview, sometimes with no AI input, sometimes with AI recommendations calibrated to match the real bias rates measured in the 2024 study (neutral, moderate, or severe). The result: **participants' own selections shifted to mirror the AI's bias**, even in the "moderate" condition calibrated to match real-world AI bias rates, not an exaggerated worst case.

This matters specifically because it undercuts a common defense of AI hiring tools — "a human is still in the loop, so it's fine." The evidence suggests the human-in-the-loop safeguard is weaker than assumed: biased recommendations don't just get rubber-stamped, they actively recalibrate what the human reviewer perceives as a reasonable choice.

## 17. A Pre-LLM Real-World Precedent: Amazon, 2018

Before generative AI, Amazon built and then scrapped an internal recruiting tool after discovering it had taught itself to penalize resumes containing the word "women's" (as in "women's chess club captain" or "women's college"), because it was trained on a decade of resumes submitted to Amazon, which skewed male in technical roles. This is one of the clearest documented cases of a company catching and killing a biased hiring algorithm before wide deployment — and it predates the current wave of LLM-based screening tools by several years, showing this is a structural risk of training on historical hiring data generally, not a problem unique to any one model generation.

## 18. Hispanic and Latino-Specific Findings — Where the Evidence Diverges

The foundational Bertrand & Mullainathan (2004) study explicitly did not test Hispanic-associated names. As one of the original researchers later explained: "We were specifically studying discrimination against Black people, so we did not include names in this experiment that are frequently associated with Hispanics or Asians." This is a real gap in the literature's foundation — most of the field built on a study that didn't measure this group at all.

A methodological complication compounds this: **Gaddis (2017)**, "Racial/Ethnic Perceptions from Hispanic Names," found that Hispanic first names paired with Anglo last names are *not* reliably recognized as Hispanic by survey respondents, while full Hispanic first-and-last-name combinations are recognized at 90%+ rates. This means earlier audit studies that used poorly chosen name pairs to signal Hispanic ethnicity may have understated real-world bias, simply because the "signal" didn't register as intended.

More recent, Hispanic-inclusive research shows two findings that point in different directions, both worth holding at once rather than resolving into a single number:

- **A 2024 study testing real LLMs directly** ("Do Large Language Models Discriminate in Hiring Decisions on the Basis of Race, Ethnicity, and Gender?") found that **acceptance rates were uniformly lowest for Hispanic male names** across every model tested — Mistral-7b, Llama2 (7b, 13b, and 70b), and GPT-3.5. In this study, Hispanic male applicants were treated worse than any other group, including Black applicants.
- **A broader global meta-analysis** (Lippens, Vermeiren & Baert, 2023), covering decades of human-reviewer correspondence-audit studies across many countries, found candidates signaling any ethnic/racial/national-origin minority status received on average 29% fewer positive responses than majority candidates — but with the *Hispanic* penalty specifically on the lower end of the range studied (8%), well below the penalty found for Arab applicants (41%) in that same body of literature.

These aren't necessarily contradictory so much as measuring different things: one is a recent, US-focused snapshot of how current LLM-based screening tools behave; the other is a multi-decade, multi-country aggregate of human-reviewer behavior. Read together, the honest takeaway is that Hispanic/Latino bias in hiring is real and documented, but less settled and less consistent across studies than the bias against Black applicants, which shows up at similar severity across nearly every study design and time period in the literature.

## 19. How Applications Surface Hispanic/Latino Identity Specifically

There is one clearly documented, federally codified mechanism for this, and it's worth understanding precisely because it's easy to assume it works like the race question — it doesn't.

Under the **Office of Management and Budget's Statistical Policy Directive No. 15**, first issued in 1977, "Hispanic or Latino" is classified as an **ethnicity**, not a race. Under the version of this standard still in effect at most employers today, that produces a genuinely separate, two-step question structure: first "Are you Hispanic or Latino?" (yes/no), then a *completely separate* race question — on which "Hispanic or Latino" does not appear as an option at all. A person can be Hispanic and select White, Black, Asian, American Indian/Alaska Native, Native Hawaiian/Pacific Islander, or more than one of those, entirely independent of the ethnicity answer.

OMB revised this standard in March 2024 to merge ethnicity and race into one combined question with Hispanic/Latino as a co-equal option (alongside a new Middle Eastern/North African category), partly in response to complaints from Hispanic respondents frustrated by the old two-question split. But federal agencies, including the EEOC, have repeatedly pushed back their compliance deadlines — as of mid-2026, the EEOC's own implementation action plan deadline has slipped to March 2027, with full form compliance not required until 2029. In practice, most applicants today are still filling out the old two-question version.

Beyond that one formally documented mechanism, ethnicity can surface through less official channels on the same application: work-authorization and visa-sponsorship "knockout" questions (which interact with assumptions about national origin tied to surname, even though work authorization itself is not ethnicity-specific), language-fluency fields common on many forms, and — as covered in Sections 11 and 18 — the parsed name field itself, which research shows functions as a direct demographic signal to both human reviewers and AI screening models regardless of whether any formal ethnicity question exists on the form at all.

## 20. EEOC Voluntary Self-Identification (Race, Disability, Veteran Status)

Private employers with 100+ employees, and federal contractors with 50+ employees and a contract of at least $50,000, are required by EEOC and OFCCP regulations to invite applicants to voluntarily self-identify race/ethnicity, gender, disability status, and veteran status.

- Completion is voluntary; declining has no legal effect on the application.
- The data is intended to be processed and stored separately from the rest of the application, used only for EEO-1 reporting, VEVRAA/Section 503 compliance, and Affirmative Action Plan purposes.
- By design, this data is not supposed to be visible to whoever is making the hiring decision.
- The disability self-ID specifically supports a federal contractor goal of having at least 7% of the workforce be people with disabilities, and applicants/employees are asked to update this status roughly every five years since disability status can change over time.

The practical seam: this data is collected through the same ATS infrastructure as everything else in the application, even though it's meant to be logically and procedurally separated from it. Worth noting: as of May 2026, the EEOC submitted a proposed rule to rescind the EEO-1 reporting requirement entirely — until that process is finalized, the current rules remain in effect.

## 21. Scale of Exposure

For context on how many people this potentially touches: estimates put AI usage in hiring at **98.4% of Fortune 500 companies**, with adoption among companies overall expected to grow from roughly 51% to 68% by the end of 2025, and over 80% of all US employers reported using some form of AI hiring tool. This is not a marginal-use-case risk — it is close to the default condition of applying for a job at a large employer in 2026.

---

# PART IV — The Legal and Regulatory Landscape

## 22. Mobley v. Workday — The Central Case

**Mobley v. Workday, Inc. (N.D. Cal., 3:23-cv-00770).** Derek Mobley alleges he was rejected from 100+ jobs applied to through Workday's recruitment systems, and attributes this to discrimination on the basis of race (Black), age (40+), and disability (anxiety/depression) — pursuing the claim against Workday itself rather than the individual employers, on the theory that Workday's AI-powered screening is the common discriminatory mechanism across all of them.

- **March 2026:** a federal judge allowed age discrimination claims under the ADEA to proceed, rejecting Workday's argument that disparate impact claims apply only to existing employees, not applicants.
- **June 2026:** Judge Rita Lin ruled Workday must face claims under California law and the federal Americans with Disabilities Act, also rejecting Workday's argument that California's anti-discrimination law shouldn't apply when applicants or jobs are located outside California.
- The case proceeds as a certified nationwide collective on the age-discrimination claims (opt-in window closed March 7, 2026); the California state-law and disability claims were revived in April 2026, widening exposure beyond age alone.
- Discovery has required Workday to produce its EEO-1 and OFCCP compliance records, while its internally curated bias-testing data was shielded under attorney-client privilege.
- Workday's public position: "Our technology looks only at job qualifications, not protected traits like race, age, or disability," and that its tools do not themselves make hiring decisions.
- The plaintiffs' theory of mechanism: bias enters through training data, model design, and evaluation criteria, even without any protected characteristic being an explicit input — years of experience can function as an age proxy, employment gaps as a disability or caregiving proxy, and educational/institutional affiliation as a race proxy. This is the exact mechanism described generically in Part III, Sections 11-12.

## 23. Related and Follow-On Cases

- **Swanson v. IBM** (filed May 2026, W.D. Texas): a 24-year IBM veteran alleges he was pushed out in a 2024 workforce reduction, then rejected for a comparable role via an AI-generated rejection, as part of an alleged strategy favoring younger "Early Professional Hires." This extends the age-bias theory to an employer's own use of AI screening, not just the vendor.
- **Harper v. SiriusXM** (filed 2025): Arshon Harper alleges he applied to roughly 150 roles and was rejected from all but one, with the AI screening allegedly relying on proxies for race — such as education and home address — to filter applicants. This maps directly onto the zip-code and university-name proxy mechanism described in Part III, Section 11.

## 24. California FEHA and Intersectionality

California's **Fair Employment and Housing Act (FEHA)** became, in 2024, the first state law to explicitly recognize **intersectional discrimination claims** — meaning a claim can be based on the combination of race and gender (or other protected categories) together, not just each in isolation. This is directly relevant given the Wilson & Caliskan finding (Section 15) that bias compounded most severely at the Black-and-male intersection specifically.

## 25. Regulatory Landscape

- **NYC Local Law 144** requires employers using "Automated Employment Decision Tools" to commission independent annual bias audits and publish the results. Responsibility sits with the employer, not just the software vendor.
- **EU AI Act** classifies hiring AI as "high-risk," with required transparency, risk-management processes, and mandatory human oversight by an August 2026 deadline.
- Colorado, Illinois, and California are rolling out or considering comparable state-level requirements.
- A December 2025 federal executive order seeks to preempt and challenge state-level AI regulation, meaning this patchwork may shift — though the underlying civil-rights statutes the Mobley case relies on (Title VII, ADEA, ADA) are long-standing federal law and unaffected by that order.

---

# PART V — The Other Side of Verification: Synthetic Identity Fraud

## 26. North Korean State-Sponsored Hiring Fraud

This section explains why ID and biometric verification in hiring has become more aggressive industry-wide. It's a response to a real, large-scale, documented fraud pattern, not arbitrary caution.

- North Korean state-sponsored operatives have used AI deepfakes and stolen or fabricated identities to obtain remote IT jobs at hundreds of Western companies, routing salaries back to the regime and in some cases stealing data or attempting extortion.
- The U.S. Department of Justice ran coordinated raids on 29 "laptop farm" operations across 16 states in mid-2025. The FBI has documented 300+ US companies that unknowingly hired DPRK operatives.
- One documented case: Christina Chapman, an Arizona resident, was sentenced to 8.5 years in prison plus restitution after hosting a laptop farm from 2020-2023 that generated over $17 million in salaries funneled to North Korea across 309 unwitting US employers, including a Fortune 500 automaker and a major media company.
- Security firm KnowBe4 unknowingly hired one such operative — he passed background checks, reference checks, and four video interviews. He was caught only when the company's endpoint detection software flagged malware being loaded onto his laptop within hours of his start date.
- Security researchers (Palo Alto Networks' Unit 42) demonstrated that a real-time video deepfake usable in an interview can be built in roughly 70 minutes by someone with no prior image-manipulation experience, using cheap consumer hardware.
- Gartner projects that by 2028, 1 in 4 candidate profiles globally will be synthetic.
- Note the documented tension here: the same facial-recognition and liveness-detection technology used to catch deepfakes carries its own bias risk. The FTC's enforcement action against Rite Aid found its AI surveillance system disproportionately misidentified women and people of color. Anti-fraud verification and anti-bias fairness can pull in opposite directions if deployed without separate auditing for each — meaning the fraud-prevention apparatus described in this section and the bias problems described in Part III are not separate issues; they intersect at the verification layer itself.

---

# PART VI — What Applicants Generally Aren't Told

## 27. The Talent Network Black Hole

When you apply and aren't selected, you're often added to a company's general talent network database. Recruiters rarely search this manually — it primarily exists to send marketing/newsletter-style emails.

## 28. Ghost Jobs

Some postings are kept open or live intentionally beyond any real, immediate hiring intent — to project growth, or to keep a standing pipeline of resumes in case of attrition. You may be applying to a role that isn't actively being filled.

## 29. "Easy Apply" Isn't a Shortcut Around Scoring

A one-click LinkedIn application is still parsed and scored through the same pipeline as a manually submitted resume. A poorly formatted LinkedIn profile can still produce a poor parse, undermining the apparent convenience of the one-click option.

## 30. Blind/Redacted Hiring Exists, But Is Opt-In

Some ATS platforms include a feature to automatically redact name, photo, address, and university from a resume before a recruiter sees it, specifically to reduce the proxy-variable bias described in Part III, Section 11. This must be actively enabled by the employer, and most do not turn it on.

## 31. EEOC Data Is Procedurally Invisible, Not Practically Invisible

The self-ID survey (Part III, Section 20) is supposed to be separated from your individual application and unseen by the person making the decision — but it is collected and stored within the same overall system as everything else, which is the seam through which procedural protections can erode in practice even when not violated in theory.

---

## Sources Referenced

- Mobley v. Workday, Inc., Case No. 3:23-cv-00770 (N.D. Cal.) — court docket, CourtListener / Free Law Project
- Reuters, TechRadar, CIO.com, Seeking Alpha — June 2026 coverage of the Mobley v. Workday ruling
- Outsolve, "Workday AI Lawsuit Explained" (April 2026)
- Warden AI, "The Workday Class Action Lawsuit" (ongoing case tracker)
- U.S. Equal Employment Opportunity Commission, eeoc.gov — Employer's Guide and EEO Self-Identification form guidance
- U.S. Department of Labor, OFCCP — Self-ID forms and VEVRAA/Section 503 guidance
- Enhancv, "Does the ATS Reject Your Resume? 25 Recruiters Explain What Really Happens" (2025)
- The Interview Guys, "The ATS Resume Rejection Myth" (2026)
- Harvard Business School, "Hidden Workers" study (2021)
- Bertrand, M. & Mullainathan, S., "Are Emily and Greg More Employable Than Lakisha and Jamal?" (2004)
- Chicago Booth Review, "This Problem Has a Name: Discrimination" — Mullainathan follow-up commentary
- Fortune, "Race discrimination in hiring: Economists' study suggests bias against Black-sounding names" (2023) — includes researcher confirmation of Hispanic/Asian name exclusion
- WBUR/Here & Now, "Name Discrimination Study Finds Lakisha and Jamal Still Less Likely to Get Hired" (2021) — Kline, Rose & Walters 83,000-application replication
- Gaddis, S.M., "Racial/Ethnic Perceptions from Hispanic Names: Selecting Names to Test for Discrimination," *Sociological Science* (2017)
- Wilson, K. & Caliskan, A., "Gender, Race, and Intersectional Bias in Resume Screening via Language Model Retrieval," AAAI/ACM AIES 2024
- Brookings Institution, summary and analysis of Wilson & Caliskan (2024/2025)
- University of Washington News, "UW research finds racial and gender bias in AI tools ranking job applicants' names" (Dec 2024)
- University of Washington News, "People mirror AI systems' hiring biases, study finds" (Nov 2025)
- "Do Large Language Models Discriminate in Hiring Decisions on the Basis of Race, Ethnicity, and Gender?" (2024)
- Lippens, L., Vermeiren, S. & Baert, S. (2023), global meta-analysis of hiring discrimination correspondence audits, as cited in "Computer says 'no': Exploring systemic bias in ChatGPT using an audit approach"
- McCormack Law Firm, "Study Finds AI Resume Screening Disadvantages Black and Female Applicants" (2025) — Amazon 2018 precedent and FEHA intersectionality note
- LegalClarity, "Why Do Applications Ask If You Are Hispanic or Latino?" and "What Are the EEOC Race Categories on the EEO-1?" (2026)
- Office of Management and Budget, Statistical Policy Directive No. 15 (1977; revised March 2024)
- Brightmine, "Ask our experts: Preparing for EEO-1 reporting" (2026)
- New York State Bar Association, "Addressing the Threat of Fake Job Candidates" (2026)
- Palo Alto Networks Unit 42, "False Face: Synthetic Identity Creation" research
- Jones Walker LLP, "Your Next Data Breach May Start With a Job Interview" (2026)
- NYC Local Law 144 (Automated Employment Decision Tools); EU AI Act, high-risk AI classification

---

*Compiled mid-2026 from the combined research and corrections developed across this project's full session.*
