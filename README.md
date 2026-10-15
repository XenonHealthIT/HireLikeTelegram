# Hire Like Telegram

This repository develops a selective, evidence-based hiring process for a small global engineering team. It borrows Telegram's emphasis on open entry, difficult assessments, realistic work, and repeated evidence while adding structured evaluation, candidate feedback, and an absolute quality bar.

## TL;DR

The assessment measures three pillars:

1. **Communication and management** — clarity, prioritization, ownership, collaboration, and response to feedback.
2. **Mathematical and logical reasoning** — quantitative fluency, structured reasoning, evidence evaluation, and problem solving.
3. **Engineering capability and experience** — coding, computer fundamentals, technical judgment, execution, and lessons demonstrated through prior and assessment work.

R1 and R3 establish the required reasoning baseline, with optional R0 available as an additional preliminary screen. R2 is the main technical filter, and R4 combines all three pillars through realistic work, revision, and structured defense. A candidate must clear the required minimum in every pillar. High performance in one pillar does not compensate for a material weakness in another, and the company may hire nobody.

## Proposed hiring process

| Stage | Assessment | Purpose |
| --- | --- | --- |
| Application | Pedigree-light eligibility review | Confirm basic requirements without filtering on prestige |
| R0 (optional) | Existing monitored SAT-like assessment | Additional preliminary general-aptitude gate when needed |
| R1 | 45–60 minute practical reasoning screen | Test applied logic, data interpretation, comprehension, and communication |
| R2 | 60–90 minute combined technical assessment | Test algorithmic coding and applied computer fundamentals |
| R3 | 60-minute mathematical problem-solving assessment | Test difficult abstract, quantitative, and proof-oriented reasoning |
| R4 | Multi-stage role evidence round | Create a realistic artifact, evaluate it blindly, revise it after feedback, and defend it in a structured interview |
| Decision | Absolute quality bar | Hire every candidate who meets the bar—or hire nobody |

Early rounds are efficient filters. R2 combines an algorithm-coding section (R2A) and a computer-fundamentals section (R2B) within one 60–90 minute assessment. The sections are scored separately: strength in coding does not erase a serious fundamentals gap, and theoretical knowledge does not compensate for non-functional code. The higher-fidelity R4 round carries more decision weight and contains four connected stages: a 3–5 hour role challenge, blind scoring with hidden tests, a 60–90 minute feedback/change stage, and an approximately 60-minute structured artifact defense.

## Pillar mapping

| Round or stage | Primary pillar | Supporting pillar(s) | Evidence collected |
| --- | --- | --- | --- |
| Application | Engineering capability and experience | Communication and management | Relevant experience, demonstrated work, eligibility, and concise written context; pedigree is not scored |
| R0 — general aptitude (optional) | Mathematical and logical reasoning | Communication and management | Additional quantitative, verbal, and analytical baseline when the existing monitored assessment is used |
| R1 — practical reasoning | Mathematical and logical reasoning | Communication and management | Applied logic, data interpretation, requirement comprehension, concise writing, prioritization, and judgment |
| R2A — algorithm coding | Engineering capability and experience | Mathematical and logical reasoning | Algorithm choice, implementation correctness, complexity, testing, and edge-case reasoning |
| R2B — computer fundamentals | Engineering capability and experience | Mathematical and logical reasoning | Applied understanding of operating systems, concurrency, networking, databases, runtimes, and security |
| R3 — mathematical problem solving | Mathematical and logical reasoning | — | Proof construction, abstraction, pattern recognition, persistence, and rigorous progress on unfamiliar problems |
| R4 Stage 1 — role challenge | Engineering capability and experience | Mathematical and logical reasoning; communication and management | Realistic execution, technical judgment, product judgment, testing, and written explanation |
| R4 Stage 2 — blind review and hidden tests | Engineering capability and experience | Mathematical and logical reasoning | Objective artifact quality, robustness, edge cases, performance, and critical failures |
| R4 Stage 3 — feedback and change | Communication and management | Engineering capability and experience; mathematical and logical reasoning | Response to feedback, adaptability, prioritization, debugging, disagreement handling, and regression control |
| R4 Stage 4 — artifact defense | Communication and management | Engineering capability and experience; mathematical and logical reasoning | Authorship, depth, tradeoff reasoning, self-awareness, ownership, and clear technical communication |
| Final decision | All three pillars | — | Separate pillar minimums plus the overall absolute quality bar |

The mapping is intentionally many-to-many. For example, coding produces engineering evidence but also exposes logical reasoning; the artifact defense evaluates communication while verifying engineering depth. Reviewers should score the relevant dimensions separately instead of converting every observation into one undifferentiated impression.

## Repository structure

```text
HireLikeTelegram/
├── README.md
├── process.md
├── deep-research-report.md
├── R1-reasoning_screen_report.md
├── R1-Instructions.md
├── R2A-Questions/
│   ├── README.md
│   ├── 01-arrays-strings.md
│   ├── 02-dynamic-trees.md
│   ├── 03-data-structures-streams.md
│   └── 04-graphs-indexing.md
├── R2B-Questions/
│   ├── README.md
│   ├── 01-os-concurrency.md
│   ├── 02-networking.md
│   ├── 03-databases.md
│   └── 04-runtime-production.md
└── R3-Questions/
    ├── README.md
    └── example-questions.md
```

### Core documents

- [`process.md`](process.md) is the authoritative description of the complete hiring pipeline, scoring principles, AI policy, and validation plan.
- [`deep-research-report.md`](deep-research-report.md) contains the research and rationale behind the overall process.
- [`R1-reasoning_screen_report.md`](R1-reasoning_screen_report.md) contains the focused research and blueprint for the practical reasoning screen.
- [`R1-Instructions.md`](R1-Instructions.md) specifies how an AI-assisted workflow should design and quality-check R1 items.

### Question banks

- [`R2A-Questions/`](R2A-Questions/README.md) contains 20 sourced, rewritten hard algorithm questions. Each includes a complete prompt, proposed solution, key cases, and a 10-point evaluation matrix.
- [`R2B-Questions/`](R2B-Questions/README.md) contains 20 sourced, scenario-based computer-fundamentals questions with answer keys, key points, and evaluation matrices.
- [`R3-Questions/`](R3-Questions/README.md) documents Putnam-, STEP-, MAT-, and IMC-style sources and contains 12 original mathematical problem-solving questions with solutions and 20-point partial-credit rubrics.

Question banks are internal assessment material. Rotate questions, add hidden tests, maintain equivalent forms, and retire leaked or poorly performing items. Pilot every assessment with strong employees before using its score as a hiring gate.
