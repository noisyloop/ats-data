# 2026 Job Reality of ATS — Reference & Dataset

A compiled, sourced reference on how Applicant Tracking Systems and AI hiring tools actually work, what bias has been documented (and how confidently), active litigation, and a companion machine-readable dataset derived from it. Compiled mid-2026. This is a folder of related files, not a git repository — there's no version history beyond what's described below, and no version control tooling is set up here.

## Files in This Folder

| File | What it is |
|---|---|
| `2026-Job-Reality-of-ATS-Complete.md` | **The current, authoritative document.** Merges and supersedes the two files below into one reference, organized into six parts: how ATS systems work internally, whether a human ever actually sees your resume, documented bias (general, disability, age, racial, and Hispanic/Latino-specific), the legal and regulatory landscape, synthetic identity fraud, and what applicants generally aren't told. |
| `ats-bias-chat-format-dataset.json` | A 25-entry instruction-tuning dataset derived from the Complete reference, in chat format (`system`/`user`/`assistant` role-content pairs). Intended for SFT-style training or evaluation pipelines, not as a standalone reading document. |
| `2026-Job-Reality-of-ATS.html` | The original ATS-mechanics document (parsing, scoring, the rejection-rate myth, EEOC self-ID, litigation, deepfake fraud, applicant-unknown facts). Content fully absorbed into the Complete `.md` — kept here for reference, not actively maintained. |
| `Racial-Bias-in-ATS-Hiring.md` | The original standalone racial- and ethnic-bias deep dive (Bertrand & Mullainathan, the UW/Wilson-Caliskan LLM study, the AI-bias-transfers-to-humans finding, the Amazon 2018 precedent, Hispanic/Latino-specific findings). Content fully absorbed into the Complete `.md` — kept here for reference, not actively maintained. |

**If you only keep one file, keep `2026-Job-Reality-of-ATS-Complete.md`.** The HTML and the standalone racial-bias `.md` are earlier drafts whose content now lives inside it.

## Sourcing and Methodology Notes

This was compiled from a mix of court dockets (primarily Mobley v. Workday, N.D. Cal. 3:23-cv-00770), EEOC and OMB federal guidance, peer-reviewed and preprint research (Wilson & Caliskan 2024, Bertrand & Mullainathan 2004, Gaddis 2017, Lippens et al. 2023, among others), recruiter-practice surveys (Enhancv, Harvard Business School), and security research (Palo Alto Networks Unit 42, the NYSBA brief on deepfake candidates).

Source quality is flagged inline throughout rather than presented uniformly. Where a claim rests on a single practitioner's estimate, a marketing-incentivized source, or an unverified social-media post, that's noted explicitly next to the claim rather than smoothed over — this applies evenly regardless of which "side" of a contested number the source supports. Two corrections made mid-compilation are preserved in the text rather than silently edited out: the original overstatement that "90-95% of applications are reviewed by a human" (Part II, Section 7), and the initial omission of depth on racial and Hispanic/Latino-specific bias, both flagged and fixed where they occur.

**This is not legal advice.** Litigation status, regulatory deadlines (NYC Local Law 144, the EU AI Act, EOC rulemaking), and recruiter practices are all time-sensitive and were accurate as of mid-2026 — verify current status before relying on any specific legal claim in either document.

## Using the JSON Dataset

The dataset is a single valid JSON array (not JSONL) of objects shaped like:

```json
{
  "messages": [
    {"role": "system", "content": "..."},
    {"role": "user", "content": "..."},
    {"role": "assistant", "content": "..."}
  ]
}
```

To convert to line-delimited JSONL (the format expected by OpenAI's fine-tuning API, Axolotl, and some HuggingFace loaders):

```python
import json

with open("ats-bias-chat-format-dataset.json") as f:
    data = json.load(f)

with open("ats-bias-chat-format-dataset.jsonl", "w") as f:
    for entry in data:
        f.write(json.dumps(entry) + "\n")
```

To load directly with HuggingFace `datasets`:

```python
from datasets import load_dataset

ds = load_dataset("json", data_files="ats-bias-chat-format-dataset.json")
```

All 25 entries share a single fixed system prompt and cover the major factual claims in the Complete reference — ATS parsing/matching mechanics, the rejection-rate debate, each documented bias category, the active litigation, EEOC self-ID rules, and synthetic identity fraud. It's a narrow, single-domain dataset; treat it as a seed set rather than a comprehensive corpus.

## Known Limitations

- The Hispanic/Latino-specific bias evidence is genuinely less consistent across studies than the Black-applicant findings — a recent LLM-specific study and an older global meta-analysis point in different directions on severity. This is presented as unresolved in the source document, not papered over.
- The "75% rejected by algorithm" vs. "8% content-based auto-reject" debate is presented as a disagreement about mechanism more than outcome, not a fully settled question — neither side currently has strong enough published methodology to call it closed.
- Court rulings referenced (Mobley v. Workday and related cases) are live litigation as of compilation. Outcomes, certifications, and even the underlying claims can change.
- The dataset is small (25 entries) and single-domain. It's useful for seeding or testing a narrow fine-tune, not for training general hiring-bias competence.
