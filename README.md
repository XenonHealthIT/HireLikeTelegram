# Hire Like Telegram

This repository develops a selective, evidence-based hiring process for a small global engineering team. It borrows Telegram's emphasis on open entry, difficult assessments, realistic work, and repeated evidence while adding structured evaluation, candidate feedback, paid finalist trials, and an absolute quality bar.

## Proposed hiring process

| Stage | Assessment | Purpose |
| --- | --- | --- |
| Application | Pedigree-light eligibility review | Confirm basic requirements without filtering on prestige |
| R0 | Existing monitored SAT-like assessment | Preliminary general-aptitude gate |
| R1 | 45–60 minute practical reasoning screen | Test applied logic, data interpretation, comprehension, and communication |
| R2A | 60–90 minute algorithm-coding assessment | Test difficult algorithmic problem solving and implementation |
| R2B | 45–60 minute computer-fundamentals assessment | Test applied knowledge of operating systems, concurrency, networking, databases, runtimes, and security |
| R3 | 45–60 minute mathematics assessment | Verify the mathematical standard required by company policy and the role |
| R4 | 3–5 hour realistic role challenge | Gather direct evidence of performance on representative work |
| R5 | Blind review and hidden tests | Score artifacts consistently and test edge cases and robustness |
| R6 | 60–90 minute feedback/change round | Measure debugging, adaptability, and response to feedback |
| R7 | Structured artifact defense | Verify authorship, depth, judgment, and communication |
| R8 | Paid half-day or one-day collaboration trial | Observe execution and collaboration with future colleagues |
| Decision | Absolute quality bar | Hire every candidate who meets the bar—or hire nobody |

Early rounds are efficient filters. Later, higher-fidelity stages carry more decision weight. R2A and R2B are separately scored gates: strength in coding does not erase a serious fundamentals gap, and theoretical knowledge does not compensate for non-functional code.

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
└── R2B-Questions/
    ├── README.md
    ├── 01-os-concurrency.md
    ├── 02-networking.md
    ├── 03-databases.md
    └── 04-runtime-production.md
```

### Core documents

- [`process.md`](process.md) is the authoritative description of the complete hiring pipeline, scoring principles, AI policy, and validation plan.
- [`deep-research-report.md`](deep-research-report.md) contains the research and rationale behind the overall process.
- [`R1-reasoning_screen_report.md`](R1-reasoning_screen_report.md) contains the focused research and blueprint for the practical reasoning screen.
- [`R1-Instructions.md`](R1-Instructions.md) specifies how an AI-assisted workflow should design and quality-check R1 items.

### Question banks

- [`R2A-Questions/`](R2A-Questions/README.md) contains 20 sourced, rewritten hard algorithm questions. Each includes a complete prompt, proposed solution, key cases, and a 10-point evaluation matrix.
- [`R2B-Questions/`](R2B-Questions/README.md) contains 20 sourced, scenario-based computer-fundamentals questions with answer keys, key points, and evaluation matrices.

Question banks are internal assessment material. Rotate questions, add hidden tests, maintain equivalent forms, and retire leaked or poorly performing items. Pilot every assessment with strong employees before using its score as a hiring gate.
