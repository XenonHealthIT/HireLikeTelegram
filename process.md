# Hiring Process

## Purpose

This process is designed for a small, global, high-talent company where every hire has disproportionate impact. It combines broad, pedigree-light entry with progressively stronger evidence of practical ability.

The process is intentionally selective, but difficulty must come from job-relevant reasoning and realistic work rather than trivia, riddles, cultural knowledge, or deliberately confusing questions. Passing one round never guarantees an offer. Candidates must meet an absolute quality bar, and the company may hire nobody from a cohort.

## Process at a glance

| Stage | Typical candidate time | Primary purpose | Decision |
| --- | ---: | --- | --- |
| Application and eligibility | 5–10 minutes | Confirm basic requirements without filtering on pedigree | Eligibility gate |
| R0 — monitored general aptitude assessment | Existing test duration | Preliminary screening using the company's SAT-like test | Gate |
| R1 — practical reasoning screen | 45–60 minutes | Measure applied logic, data reasoning, comprehension, and communication | Gate |
| R2A — algorithm coding | 60–90 minutes | Efficiently filter for algorithmic problem solving and implementation strength | Primary coding gate |
| R2B — computer fundamentals | 45–60 minutes | Verify practical command of core computing concepts | Primary knowledge gate |
| R3 — mathematics assessment | 45–60 minutes | Measure the required level of mathematical fluency | Gate |
| R4 — role evidence round | 5–7.5 hours across multiple stages | Evaluate realistic work, robustness, revision, authorship, and judgment | Major score |
| Final decision | — | Apply the absolute hiring bar across all evidence | Hire / no hire |

## Entry principles

- Accept applications globally where employment constraints allow.
- Use the résumé primarily for eligibility and context, not prestige filtering.
- Do not prefer candidates merely because of a particular school, employer, nationality, professional network, or résumé style.
- Give candidates clear information about the stages, expected time, permitted tools, accommodations, and data handling before they begin.
- Use multiple equivalent test forms or controlled scheduling windows so that geography and time zone do not become selection criteria.

## R0 — monitored general aptitude assessment

The company will retain its existing monitored SAT-like assessment as the preliminary screen. It should establish a broad baseline in general reasoning, language, and quantitative ability before the company spends significant reviewer time on a candidate.

Operational requirements:

- Apply the same published administration rules to every candidate.
- Provide reasonable accommodations and an alternative process when standard monitoring is not accessible.
- Keep identity verification and monitoring proportionate to the risk being controlled.
- Set the passing threshold before reviewing a cohort's results.
- Periodically check whether the test predicts success in later rounds and whether it excludes groups in ways unrelated to job performance.
- Do not use an exceptionally high R0 score to compensate for failure in later, job-relevant rounds.

R0 is a preliminary gate, not a final measure of candidate quality.

## R1 — practical reasoning screen

This is a 45–60 minute applied reasoning assessment for knowledge work. It is not another general intelligence test. Its material should resemble the information and decisions encountered at work.

Recommended weighting:

| Construct | Weight | Example task |
| --- | ---: | --- |
| Logical problem solving | 30% | Resolve constraints, identify implications, or diagnose inconsistent information |
| Quantitative and data reasoning | 25% | Interpret graphs, rates, percentages, capacity, and uncertainty |
| Written comprehension | 20% | Extract requirements and ambiguities from realistic material |
| Written communication | 15% | Produce or select a concise, accurate explanation |
| Role-specific mini-items | 10% | Read code, exercise product judgment, or perform role-specific analysis |

A typical 55-minute form may contain:

- 15 minutes of logical constraint and diagnostic questions;
- 12 minutes of quantitative and data questions;
- 9 minutes of requirement-comprehension questions;
- 8 minutes of written-communication questions;
- 6 minutes of role-specific mini-items; and
- 5 minutes for instructions and review.

Questions must be original, resistant to simple searching, understandable without country-specific knowledge, and supported by a defensible answer and scoring guide. They must not depend on riddles, trick wording, obscure vocabulary, advanced mathematics unrelated to the role, or spatial reasoning unless the job actually requires it.

R1 is a minimum-capability gate. It should not dominate the final hiring decision.

## R2 — technical fundamentals filter

R2 is one of the primary filters for technical candidates. Its purpose is to identify candidates who lack the minimum coding fluency or computer-science foundations needed for the role before engineers spend time reviewing substantial projects or conducting interviews. It is divided into two independently scored components: R2A for algorithm coding and R2B for computer fundamentals.

### R2A — algorithm coding

R2A contains one hard or hard-medium LeetCode-style problem, or two shorter problems of equivalent total difficulty. It assesses:

- algorithm selection and explanation;
- functional correctness, including hidden edge cases;
- time and space complexity;
- command of core data structures;
- code clarity and testing discipline; and
- the ability to recognize when a straightforward solution will not meet the constraints.

Candidates may choose from the programming languages supported by the evaluation environment unless the role specifically requires one language. The bank in `R2A-Questions` contains sourced, rewritten assessment variants with solutions and scoring guides.

R2A scoring:

| Dimension | Suggested weight |
| --- | ---: |
| Correctness, including hidden cases | 40% |
| Problem solving and algorithm choice | 25% |
| Complexity and resource awareness | 15% |
| Code clarity | 10% |
| Testing and edge-case discipline | 10% |

### R2B — computer fundamentals

R2B is separate from the coding exercise. It uses scenario-based short-answer and multiple-select questions covering a role-appropriate selection of:

- operating systems and resource management;
- processes, threads, concurrency, and memory visibility;
- networking, DNS, HTTP, and TLS;
- databases, transactions, indexes, locking, and query plans;
- runtimes and garbage collection;
- containers and production resource controls; and
- basic application security.

The question bank in `R2B-Questions` provides sourced prompts, answer keys, key points, and scoring guides. A form should sample across domains rather than overfitting to a candidate's preferred technology. Questions should test applied diagnosis and tradeoffs, not definitions recalled without context.

R2B scoring:

| Dimension | Suggested weight |
| --- | ---: |
| Technical correctness | 40% |
| Causal reasoning and diagnosis | 25% |
| Practical mitigation or design choice | 20% |
| Tradeoff awareness | 10% |
| Communication precision | 5% |

R2A and R2B have separate minimum thresholds. A strong fundamentals score cannot compensate for non-functional code, and a strong coding result cannot compensate for serious gaps in fundamentals required by the role. Critical failures include fabricated output, prohibited outside assistance, or a solution that cannot run in the stated environment.

Because R2 is a high-volume filter, R2A normal-case and hidden-test scoring and the objective portions of R2B should be automated where possible. Human review should focus on explanations, borderline results, suspected assessment problems, and integrity checks.

## R3 — mathematics assessment

All candidates complete a dedicated mathematics round as required by company policy. The assessment should have a documented purpose and a level appropriate to the role.

The common core may cover:

- arithmetic, ratios, percentages, and estimation;
- algebraic manipulation;
- probability and basic statistics;
- interpretation of functions, tables, and graphs; and
- multi-step quantitative reasoning.

Role-specific modules may add discrete mathematics for software roles, linear algebra and probability for machine-learning roles, or other mathematics that is genuinely required by the work. Advanced topics should not be included merely to make the test harder.

Use a separately reported math score rather than hiding it inside a general score. Establish a minimum threshold in advance, pilot the test with strong current employees, and review whether the threshold distinguishes job performance. The math result should be treated as a gate where company policy requires it, while the role challenge remains the strongest evidence of actual job performance.

## R4 — role evidence round

R4 is one continuous round built around the same candidate artifact. It has four stages: initial creation, blind evaluation, revision after feedback, and structured defense. Keeping these activities together makes their relationship explicit and avoids treating four observations of the same work as unrelated rounds.

### Stage 1 — realistic role challenge

Candidates who pass the screening rounds receive a three-to-five-hour challenge within a broader scheduling window. The task should resemble work they might encounter during their first three months, while using synthetic, open-source, or deliberately isolated material rather than commercially useful unpaid work.

For a software engineer, a challenge might ask the candidate to:

> Work in an unfamiliar repository, implement a feature without breaking backward compatibility, satisfy visible and hidden tests, remain within a stated performance budget, and submit a short note explaining the important tradeoffs.

The candidate should receive:

- a clear problem statement and deliverables;
- a repository or realistic working artifact;
- normal-case examples or visible tests;
- meaningful constraints;
- a stated timebox and submission procedure;
- an explicit AI and outside-resource policy; and
- a rubric summary so expectations are not mysterious.

Recommended engineering rubric:

| Dimension | Weight |
| --- | ---: |
| Functional correctness | 25% |
| Robustness and edge cases | 20% |
| Architecture and code quality | 15% |
| Performance and resource discipline | 10% |
| Product judgment | 10% |
| Testing discipline | 10% |
| Explanation and tradeoffs | 10% |

Define critical failures independently of the numerical score. Examples include a major security vulnerability, destructive data handling, fabricated results, an un-runnable submission, or complete violation of a core requirement.

### Stage 2 — blind scoring and hidden tests

The initial artifact review is anonymous wherever feasible. Reviewers see a candidate identifier, submission, test results, and explanation, but not the candidate's name, school, nationality, photograph, or previous employers.

Evaluation rules:

- Run the same visible and hidden test suite for equivalent submissions.
- Have at least two assessors independently score important artifacts before discussing them.
- Record scores and evidence against the rubric rather than relying on an overall impression.
- Resolve large reviewer disagreements through documented review.
- Reveal candidate identity only after the initial artifact score is locked.
- Do not rank candidates solely against one another; compare each candidate with the predefined quality bar.

Hidden tests should cover realistic edge cases, regressions, performance constraints, malformed input, and other important behaviors not completely specified by the visible examples. They should not depend on arbitrary interpretations that a reasonable candidate could not infer.

### Stage 3 — feedback and change round

Candidates who meet the role-challenge bar receive a 60–90 minute revision task. Give every candidate an equivalent combination of:

- one defect or failed hidden test;
- one changed requirement; and
- one quality constraint, such as latency, reliability, accessibility, or maintainability.

Evaluate whether the candidate:

- understands the feedback correctly;
- isolates the underlying problem;
- produces a proportionate fix;
- avoids regressions;
- updates tests and documentation;
- communicates what changed; and
- respectfully challenges feedback when it is incorrect or unsafe.

This stage measures rate of improvement, judgment under change, and ability to work with review—not blind obedience.

### Stage 4 — structured artifact defense

The structured defense verifies that the candidate understands and owns the submitted work. It also gathers consistent evidence about technical depth, judgment, learning, and communication.

Every candidate receives the same core prompts, adapted only where their artifact requires a specific follow-up:

1. Walk through the hardest decision you made. What alternatives did you reject and why?
2. Which part of your submission are you least confident about?
3. If demand increased tenfold, what would fail first?
4. Diagnose one hidden test or scenario your submission did not handle.
5. What unrelated issue did you notice, and how would you handle it without losing control of scope?
6. How would you resolve a disagreement with a colleague whose criticism is partly correct?
7. What did you learn that would change your approach if you restarted?

Interviewers must use behavioral anchors. A high score requires accurate explanation, recognition of non-obvious tradeoffs and limitations, and appropriate updating when presented with new evidence. Two assessors should score independently before holding a decision discussion.

## Tool and AI policy

Assessment rules should mirror the working environment as closely as possible.

- For monitored R0 and any closed-book portions of R1, R2, or R3, clearly state which tools are prohibited.
- For the role challenge, permit the tools employees would normally use, including AI where appropriate.
- Require candidates to disclose material AI assistance and accept responsibility for every submitted decision and line of code.
- Use the defense and change round to verify understanding and authorship.
- Do not rely on surveillance alone to establish integrity.

## Final decision

The hiring committee reviews independently scored evidence from all required stages. Later, higher-fidelity evidence should receive more weight than early screening scores.

Recommended decision rules:

- Each required gate and minimum subscore must be met.
- No unresolved critical failure may remain.
- All four stages of R4 form the core hiring evidence and should be reviewed together.
- Pedigree, charisma, and cohort rank cannot override failure to meet the quality bar.
- A candidate who meets the absolute bar may be hired even if another candidate scores higher.
- The company may hire nobody when no candidate meets the bar.

Thresholds should be defined before candidate identities are revealed and should initially be treated as pilot parameters rather than scientifically validated constants.

## Quality control and validation

Before launch, have a representative group of strong employees complete every new assessment under candidate conditions. Use the results to identify ambiguous questions, unrealistic time limits, weak hidden tests, and accidental dependence on company-specific knowledge.

Track:

- item difficulty and discrimination;
- completion and abandonment rates;
- time per item and per stage;
- reviewer disagreement;
- conversion between stages;
- candidate time and company review time;
- accommodations and assessment incidents;
- candidate experience;
- offer acceptance;
- ramp time, retained performance, and relevant work-quality outcomes; and
- whether stage scores predict later assessment and job performance.

Review the process after the first 30–50 serious candidates and after each subsequent hiring cohort. Retire leaked, ambiguous, or non-predictive items; maintain equivalent forms; and change thresholds only through a documented review rather than in response to the strength of a particular cohort.

The assessment system is a maintained company product. Its goal is not to maximize rejection. Its goal is to accumulate reliable evidence that a candidate can produce exceptional work, improve under feedback, explain their decisions, and strengthen a small team.
