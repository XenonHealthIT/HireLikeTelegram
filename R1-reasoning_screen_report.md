# Designing a Telegram-Style Practical Reasoning Screen

## Executive findings

The most useful discovery is that Telegram itself published unusually detailed guidance on what it considered a good aptitude assessment. In its 2021 **Aptitude Test Contest**, Telegram asked participants to create tests covering English, mathematical ability, and spatial/logical thinking. Crucially, Telegram stated that its public sample tests were **“inspired by assessments which Telegram staff are required to score highly on.”** That makes this the closest first-party public evidence I found about the philosophy behind Telegram's internal reasoning assessments, although it does **not** establish that Telegram still uses the identical test or syllabus in 2026. citeturn23view0

Telegram's design rules are remarkably sensible. Questions were to be original, resistant to simple web search, globally understandable without local knowledge, varied rather than repetitive, free of riddles and tricks, equipped with plausible distractors, and accompanied by explanations. Mathematical questions were supposed to emphasize everyday quantitative reasoning; logical questions were explicitly supposed to emphasize problem solving rather than pure mathematics. Telegram also instructed test designers to pilot questions on people, record which items they got right and wrong, adjust timing and difficulty, then subject the assessments to structured peer review. citeturn23view0turn23view1turn24view0

My main recommendation, however, is **not to clone Telegram's old aptitude test literally**. Modern personnel-selection research provides a reason to move one step closer to actual work. Revised meta-analytic research by Sackett, Zhang, Berry, and Lievens found that the predictive validity of many selection methods had previously been overstated; structured interviews became the highest-ranked method in their revised analysis, while work samples and cognitive-ability tests remained useful but lower than previously believed. Their applied follow-up emphasizes that several of the strongest methods are comparatively job-specific. citeturn18search0turn18search11

For your company, I would therefore define the first screen as:

> **An original, difficult but learnable set of short, job-adjacent problems that tests whether a candidate can extract relevant information, reason from evidence, work within constraints, diagnose causes, and revise a plan when circumstances change—without relying on specialist trivia.**

That is much closer to OECD's contemporary concept of **adaptive problem solving**, which deliberately tests solving non-routine problems and adapting when new information changes the situation. OECD's released “Best Route” task, for example, initially asks a participant to satisfy several scheduling and route constraints, then changes the situation so the original solution must be reconsidered. citeturn16search0turn16search1

For a first implementation, I recommend a **45-minute screen containing approximately 15 scored questions plus 3 unscored experimental questions**, drawing from five reasoning families:

| Reasoning family | Proposed weight | What it measures |
|---|---:|---|
| Evidence and argument reasoning | 20% | Can the candidate distinguish evidence from assertion, find assumptions, and update conclusions? |
| Data interpretation | 25% | Can they interpret tables, metrics, graphs, rates, and incomplete data correctly? |
| Constraints and planning | 20% | Can they find a feasible or optimal solution under multiple constraints? |
| Diagnosis and causal reasoning | 20% | Can they discriminate between competing explanations and choose useful next evidence? |
| Adaptive reasoning | 15% | Can they revise a previously sensible decision when one important fact changes? |

Those percentages are **my recommended blueprint**, not an industry standard. They deliberately shift the emphasis away from classic IQ-test mechanics such as long runs of number sequences and abstract shape puzzles and toward reasoning closer to the decisions a high-autonomy employee actually makes.

The deeper conclusion from this research is therefore:

**Use Telegram's principles, OECD/GMAT/LSAT/Civil Service items as design references, and psychometric standards as the engineering discipline—but build and calibrate your own proprietary question bank.**

Public problem banks are excellent for learning how good questions work. They are generally poor choices for a live high-stakes hiring screen because exposure creates practice effects, searchability undermines interpretation, and some sources prohibit commercial reuse. A meta-analysis of retesting on cognitive tests covering 107 samples and 134,436 participants found a mean practice effect of 0.26 standard deviations, with larger effects when identical forms were reused and when candidates received coaching. citeturn17search6


## What Telegram's own assessment guidance tells us

Telegram's 2021 material is more useful than anecdotes about its hiring because it effectively constitutes a miniature **item-writing manual**.

Telegram's contest required three 30-question quizzes: one in English, one in mathematics, and one split into 15 spatial and 15 logical questions. For mathematical ability it specified everyday arithmetic, graphs, ratios, percentages and basic algebra rather than esoteric mathematics. For logical thinking, it explicitly said to focus on **problem-solving skills**; mathematics could occur inside a logical problem but should not itself be the point of the question. citeturn23view0

More important than the categories are the quality rules.

| Telegram rule | What it implies for your screen |
|---|---|
| Questions must be original | Do not assemble a live test by scraping puzzle websites |
| Candidates should not gain an advantage from Google | Make the solution depend on reasoning over supplied information |
| No local knowledge | Avoid geography, idioms, history trivia, local regulations and culturally specific assumptions |
| Don't rely heavily on one mechanic | Measure the construct using several different task forms |
| No riddles or trick questions | Difficulty should come from reasoning, not deception |
| Plausible alternatives | Wrong answers should correspond to realistic reasoning mistakes |
| Explain every answer | Every live item should have a documented solution rationale |
| Non-basic formulas should be supplied | Separate reasoning skill from memorized school knowledge |
| Target strong adults, but not “only geniuses” | Items need useful discrimination rather than theatrical impossibility |
| Typically about one or two minutes per question | Keep most screening items compact, reserving longer times for richer mini-cases |

These are directly reflected in Telegram's contest rules. citeturn23view0

Telegram was also explicit that **“inventive” does not mean weird**. It encouraged novel question formats but required designers to be able to justify why a new mechanic added assessment value. It warned against overusing number sequences or “which shape is different?” questions. citeturn23view0

That is an important distinction for a company hoping to create a famously difficult assessment. There are two kinds of difficulty:

**Good difficulty** comes from having to combine facts, identify a hidden constraint, distinguish plausible hypotheses, reject an attractive but unsupported conclusion, or respond to changing information.

**Bad difficulty** comes from obscure vocabulary, excessive arithmetic, ambiguous wording, trivia, deliberate traps, microscopic diagrams, missing assumptions, or a timer so aggressive that the test primarily measures reading speed.

Telegram's own peer-review rubric actually treated questions that were too easy **or too hard**, misleading questions, implausible distractors, copied questions, poor media, and excessive reliance on one mechanic as assessment defects. citeturn24view0turn24view1

The contest also contains an excellent model for your internal item-development process. Telegram told designers to test their quizzes on several people, record average results and item-level successes/failures, adjust the questions, and then perform another end-to-end review. citeturn23view1 It subsequently had participants peer-review other tests against an explicit defect taxonomy covering difficulty, timing, ambiguity, multiple valid answers, incorrect keys, weak distractors, originality, explanations, media, local knowledge and repetitive mechanics. citeturn24view0turn24view1

This suggests that the most valuable part of the “Telegram model” is arguably not the exact puzzle types. It is the **assessment-development culture**:

**original problem → explicit solution → pilot → critique → revision → live use → continued replacement.**

That is the element I would copy most faithfully.


## Existing problem bases worth studying

There is no single public repository I would recommend importing wholesale into a commercial hiring assessment. There are, however, several exceptionally good **reference libraries** from which your item writers can learn different aspects of practical reasoning.

| Source | Particularly useful for | Public examples? | Suitability for copying into your live test |
|---|---|---:|---|
| Telegram Aptitude Test materials | Telegram-style philosophy, logic, quantitative/spatial items, quality criteria | Yes | **Study structure; create originals** |
| OECD PIAAC Adaptive Problem Solving | Dynamic situations, constraints, new information, digital environments | Yes | Excellent structural model; verify reuse rights before commercial reproduction |
| OECD PISA | Applied quantitative/scientific/digital problem solving | Yes | Excellent inspiration; do not assume public release means unrestricted commercial reuse |
| GMAT Data Insights | Multi-source reasoning, data sufficiency, tables and graphs | Samples/prep available | Copy the format concept, not proprietary questions |
| LSAT Logical Reasoning | Assumptions, flaws, inference, strengthening/weakening evidence | Yes | Excellent argument-reasoning taxonomy; write original content |
| UK Civil Service tests | Verbal/numerical reasoning, adaptive delivery, pilot items, accessibility | Practice tests | Excellent operational benchmark |
| EPSO/EU Careers | Multilingual verbal, numerical and abstract reasoning | Yes | Particularly useful for global/localization thinking |
| Project Euler | Hard quantitative/computational problem construction | Large archive | **Do not use commercially without appropriate permission** |

### Telegram's aptitude-test material

This should be your starting point because of the direct connection to the strategy you are trying to emulate. Telegram required originality, explanations, globally understandable scenarios, varied mechanics, sensible timing and search resistance, and its peer-review scheme gives you a ready-made checklist for reviewing new questions. citeturn23view0turn24view0

I would **not** turn Telegram's sample questions into your problem bank. The right thing to copy is its item-writing philosophy.

### OECD PIAAC Adaptive Problem Solving

For the construct you called “practical reasoning,” this is probably the strongest public source I found.

The OECD publishes released items from the Programme for the International Assessment of Adult Competencies, including interactive adaptive-problem-solving tasks. Its released-item documentation does more than show the question: it gives the problem description, possible solution paths, cognitive process, functionality, framework classification, answer/scoring information and, where available, proficiency level. citeturn16search1

The standout model is **Best Route**. The candidate uses an interactive map while satisfying several goals and time constraints. In a subsequent item, the situation changes, producing new constraints and requiring adaptation rather than simply repeating the original solution. citeturn16search0

That pattern is almost ideal for hiring:

> Situation → candidate makes decision → one fact changes → candidate must update rather than defend the previous answer.

PIAAC's broader framework also separates problem solving into stages such as defining the problem, searching for a solution and applying a solution, while varying complexity through the number of interacting elements, the dynamics of the situation, characteristics of the information environment and context. More dynamic and less structured information increases the need for monitoring and adaptation. citeturn14view2turn14view4

For your purposes, this provides an excellent **difficulty dial**:

| Easier practical reasoning | Harder practical reasoning |
|---|---|
| Few variables | Several interacting variables |
| Relevant information obvious | Relevant and irrelevant information mixed |
| Static conditions | Conditions change |
| One obvious constraint | Several simultaneous constraints |
| One-step decision | Multi-step dependency |
| Clear causal evidence | Several plausible explanations |
| Current state only | Must anticipate downstream consequences |

OECD's highest adaptive-problem-solving levels emphasize complex and dynamic situations, multiple constraints, distinguishing important changes from trivial ones, anticipating future system behavior and adapting strategy. citeturn14view1

That is a far better model for a “hard” assessment than merely increasing arithmetic complexity.

### OECD PISA

PISA's released-question library is another excellent design reference because it contains interactive mathematics, science, digital-learning, financial-literacy, creative-thinking and collaborative-problem-solving tasks. The current OECD library includes released 2025 science and Learning in the Digital World items as well as earlier problem-solving domains. citeturn21search0turn21search11

The reason to study PISA is not that your candidates should answer school questions. It is that PISA is very good at constructing a **self-contained world** in which the candidate is given the information necessary to reason.

That is precisely what a global hiring assessment should do. Instead of:

> “Do you already happen to know this?”

the item asks:

> “Given these facts, what can you work out?”

### GMAT Data Insights

GMAT's current Data Insights section offers perhaps the best taxonomy for building compact data-oriented business problems. It includes **Data Sufficiency, Multi-Source Reasoning, Table Analysis, Graphics Interpretation and Two-Part Analysis**. GMAC describes these tasks as requiring candidates to combine graphic, numeric and verbal information to make informed decisions. citeturn19search2

Those formats transfer extremely well into employment testing.

For example:

**Data Sufficiency** becomes: *Do we actually have enough evidence to make this operational decision?*

**Multi-Source Reasoning** becomes: *The dashboard, customer report and system log appear to tell different stories. What follows from all three?*

**Table Analysis** becomes: *Which customers/projects/servers meet a particular combination of constraints?*

**Two-Part Analysis** becomes: *Which diagnosis and next action are jointly consistent?*

The intellectual property should remain yours; use these as **format patterns**, not a source from which to copy questions.

### LSAT Logical Reasoning

LSAT material is an excellent source for argument-reasoning archetypes. Official LSAC questions test such skills as identifying what follows from evidence, detecting assumptions or flaws, determining what additional evidence strengthens or weakens an argument, and comparing reasoning patterns. citeturn19search3

A company version need not look legal or academic. The same logical structures can be embedded in operational contexts:

> A metric fell after a deployment. Does that establish causation?

> A team argues feature A is responsible for retention because users of A retain better. What assumption is being made?

> Which new piece of evidence most strongly distinguishes hypothesis X from hypothesis Y?

These are much more “practical” than asking candidates to identify the formal name of a logical fallacy.

LSAC also uses an **unscored experimental section to validate future questions**, explicitly describing it as important to the validation and fairness of new items. citeturn19search8 That is a practice worth adopting in miniature.

### UK Civil Service and EPSO

The UK Civil Service's online verbal and numerical tests are especially instructive operationally. Its verbal items ask candidates to draw conclusions from provided written information; numerical items use tables, graphs and other numerical information. The tests include unscored trial questions used to calibrate future items, provide practice questions in advance, and are computer adaptive. citeturn19search0turn19search1

The Civil Service also makes an important distinction that your company should consider: its current verbal/numerical tests are not time-limited, meaning it is attempting to emphasize reasoning accuracy rather than raw speed. citeturn19search0

I would not necessarily make your screen untimed, but this illustrates a key principle: **only make speed part of the score when speed is part of the construct you actually care about.**

EPSO, the European Personnel Selection Office, provides public verbal, numerical and abstract-reasoning examples and makes verbal/numerical samples available across the EU's official languages, with accessible versions also provided. citeturn20search0turn20search1

For a company committed to global hiring, that is a useful reminder that **English proficiency and reasoning ability are separable constructs**. If sophisticated English is genuinely required for the job, testing it is reasonable. If not, unnecessarily difficult prose can cause your reasoning test to become partly a language test.

### Project Euler

Project Euler's archive is useful for teaching item writers what elegant quantitative problems look like, especially for technical roles. But it should not become your commercial question bank. Project Euler explicitly licenses its main problems under **CC BY-NC-SA 4.0** and states that the problems must not be used commercially. citeturn21search2

This illustrates a broader rule: **publicly visible does not mean commercially reusable**.

For every source above, I would maintain a strict policy that external questions may be studied for mechanisms and taxonomies, but production items must either be original or explicitly licensed for your commercial use.


## How good practical-reasoning questions should be structured

The formal assessment literature largely supports Telegram's instincts, while providing a more rigorous framework for implementing them.

SIOP's *Principles for the Validation and Use of Personnel Selection Procedures* is an authoritative professional guideline for employee-selection testing and was approved by the APA Council of Representatives. The basic principle is that the interpretation and use of a selection procedure should be supported by evidence relevant to the job and purpose for which it is being used. citeturn17search0

For your team, this means the assessment-development process should begin **before writing puzzles**.

First define what successful people in your unusually small, high-autonomy organization actually have to reason about. For example:

> They receive incomplete information.

> They need to identify the important constraint without being told.

> They make decisions without waiting for extensive managerial direction.

> They distinguish correlation from causation.

> They rapidly discard a plan when evidence contradicts it.

> They can understand an unfamiliar system from documentation.

Those become your target reasoning behaviors.

Then create item specifications that reproduce those cognitive operations in miniature.

ETS's published quality standards provide an excellent process model. They call for an explicit test blueprint covering the content and skills being assessed, the source of those requirements, representation of the domain, test length and formats, timing, item-development and review processes, pretesting, psychometric properties, administration, scoring and accessibility considerations. citeturn12view0turn12view1

ETS further recommends that items be written to specifications so that irrelevant factors are minimized, reviewed by qualified reviewers, and pretested on people representative of the target population when feasible. Reviews should cover content, links to the intended task/construct, instructions, scoring, fairness, accessibility, difficulty and presentation. citeturn12view1turn12view2turn12view3

I would turn those principles into a fixed **item specification card** for every question in your bank:

| Field | What the item writer must document |
|---|---|
| Construct | Exactly what reasoning behavior is being tested |
| Scenario | The self-contained problem situation |
| Required information | What the candidate actually needs |
| Distractor information | What is irrelevant but plausible |
| Reasoning path | Steps required to derive the answer |
| Correct answer | Unambiguous key |
| Distractor rationale | Why a smart candidate might select each wrong option |
| Knowledge assumptions | What prior knowledge, if any, is required |
| Difficulty lever | What makes this item harder than an easier version |
| Time expectation | Expected solving time |
| Accessibility risks | Visual, language, motor or other concerns |
| Localization risks | Currency, idiom, cultural assumptions, units |
| Search/AI exposure | Whether the answer can simply be retrieved |
| Reviewer status | Independent solution checks |
| Pilot statistics | Difficulty/discrimination once data exist |
| Version history | Any modifications after pilot/live exposure |

The **distractor rationale** is especially important. Telegram explicitly objected to obviously wrong alternatives because they let candidates reverse-engineer the correct answer rather than solve the problem. citeturn24view0

For each wrong option, the item author should be able to say something like:

> Candidate chooses B if they ignore the capacity constraint.

> Candidate chooses C if they compare totals rather than rates.

> Candidate chooses D if they infer causation from temporal order.

That converts multiple-choice questions from trivia into **diagnostic reasoning items**.

A good practical-reasoning question should therefore have the structure:

**Situation → objective → information → constraints → decision → plausible competing responses.**

A harder version should generally add one of four things:

**Interaction:** two facts must be considered together.

**Noise:** some supplied information is irrelevant.

**Uncertainty:** the evidence supports probabilities rather than certainty.

**Change:** new evidence invalidates part of the original solution.

It should generally **not** become harder by requiring more obscure factual knowledge.


## Recommended screen and question architecture

I would create a **45-minute Practical Reasoning Screen** as the first serious hurdle after basic eligibility screening.

The difficulty should be high enough that a strong candidate cannot answer mechanically, but the test should not be designed so that “almost everyone fails.” A hiring screen needs to distinguish meaningfully among candidates around the level where you intend to make decisions; difficulty for its own sake provides little measurement value. Telegram's own rubric treated questions that were excessively difficult as quality problems, and ETS standards emphasize pretesting and analyzing item difficulty and test functioning. citeturn24view0turn12view3

A practical first blueprint would be:

| Component | Scored items | Approx. time | Example cognition |
|---|---:|---:|---|
| Evidence & inference | 3 | 6 min | What actually follows from the facts? |
| Data interpretation | 4 | 10 min | Read metrics, rates, tables and charts |
| Constraints & planning | 3 | 9 min | Find a feasible or best plan |
| Diagnosis | 3 | 9 min | Distinguish hypotheses, choose next evidence |
| Adaptive problems | 2 | 7 min | Update after new information |
| Experimental items | 3 | Embedded | Future-bank calibration |
| Instructions/practice buffer | — | ~4 min | Format familiarization |

**Total: 15 scored + 3 unscored pilot items in approximately 45 minutes.**

The exact length should be adjusted after empirical piloting. Telegram itself recommended setting timing by observing which questions testers failed to complete rather than mechanically giving every item the same amount of time. citeturn23view0turn23view1

I would use the following item families.

**Evidence inference.** Give a compact scenario containing six or seven facts. Ask what must be true, what is merely possible, or what conclusion is unsupported. This borrows the good part of LSAT-style reasoning while using your own operational context. citeturn19search3

**Data sufficiency.** Give a decision plus several available data sources. Ask whether the supplied evidence is sufficient and, if not, which additional measurement is required. This adapts GMAT's Data Sufficiency concept to actual business judgment. citeturn19search2

**Multi-source reconciliation.** Provide an email, a small metrics table and perhaps a system status note. Ask which conclusion is compatible with all sources. GMAT's Multi-Source Reasoning provides a mature model of this format. citeturn19search2

**Constraint scheduling.** Give five tasks, several dependencies and a resource limit. Ask which schedule works, or which one minimizes completion time. Then occasionally add a new constraint in a second item. This is directly analogous to the useful structure of PIAAC's adaptive “Best Route” problem. citeturn16search0

**Causal diagnosis.** Give a system in which something went wrong and several observations. Ask which hypothesis remains viable, which experiment would best discriminate between two hypotheses, or which datum would most change the diagnosis.

**Prioritization under uncertainty.** Give five candidate actions with different costs, expected benefits, reversibility and information value. Ask which action is rational first. This gets much closer to the decision making of a small autonomous team than a standard IQ puzzle.

**Rule induction.** Give candidates the rules of an unfamiliar system through examples rather than expecting prior knowledge. Then ask them to reason about a new case. This tests rapid learning while keeping specialist knowledge out of the equation.

**Update questions.** Present a defensible decision, then reveal a new fact. Ask the candidate to revise the answer. OECD explicitly treats adaptation to changes in a problem situation as central to adaptive problem solving. citeturn16search0turn16search19

A particularly good item family for your philosophy would be the **“best next question” problem**:

> You cannot yet determine the answer. Which single piece of information would be most valuable to obtain?

That measures something elite small teams require constantly: recognizing that the correct action is sometimes not to decide immediately, but to reduce the right uncertainty.

### An illustrative original item pattern

Imagine the candidate receives:

> A service's error rate rose from 0.4% to 2.1% at 14:00.  
> A new version was deployed to 30% of servers at 13:50.  
> Traffic increased 40% at 13:55.  
> Error rates are 5.8% on the new version and 0.5% on the old version.  
> The new servers receive a somewhat larger share of mobile traffic.

Then ask:

**Which observation would most strongly distinguish “the deployment caused the increase” from “the increase is caused by the different traffic mix”?**

The best response would be something like **comparing error rates between new and old versions within the same traffic category**.

Notice why this is better than “What is the next number in this sequence?”

The candidate has to understand confounding, identify competing causal models, and choose information that discriminates between them. No specialized systems-engineering knowledge is necessary because the relevant facts are contained in the question.

A second item could then reveal that the within-category difference persists and ask which action is now best justified.

That gives you **reasoning plus adaptation** in a single micro-case.


## Building a proprietary problem bank

The strongest long-term strategy is to treat the question bank as an internal product rather than a document HR writes once.

I would establish an initial target of roughly **120–150 production-quality items** before the assessment becomes a major global hiring channel. That number is my operational recommendation rather than a published standard. It gives you enough material to create multiple overlapping forms, replace compromised items, experiment with new formats and avoid repeatedly exposing the same small pool.

The development funnel should be much larger because many drafted questions should die during review.

A realistic workflow would be:

**Item brief → independent solution → editorial review → adversarial review → small pilot → revision → unscored live pilot → calibrated bank → scored production → periodic monitoring → retirement.**

Telegram's own assessment-design contest followed a surprisingly similar philosophy: creation, private testing, revision, peer review, rebuttal and final review. citeturn23view1turn23view2 ETS similarly recommends item specification, expert review, pretesting with the intended population and post-administration evaluation. citeturn12view1turn12view2turn12view3

I would create an internal **red-team review** that tries to break each item before candidates ever see it. Reviewers should attempt to:

find an alternative valid answer;

solve it using an unintended shortcut;

identify assumptions not stated;

Google characteristic phrases;

ask an LLM for the answer;

identify cultural assumptions;

misread the graphic in a reasonable way;

solve it without demonstrating the intended construct;

determine whether one distractor looks linguistically different from the others;

check whether reading difficulty overwhelms reasoning difficulty.

This is a more rigorous version of Telegram's published defect checklist, which explicitly covered multiple correct answers, incorrect official answers, misleading questions, weak alternatives, copied material, inadequate explanations, local knowledge, poor media and repetitive mechanics. citeturn24view0turn24view1

### Use experimental questions continuously

I would place **2–3 unscored new items** into every candidate's screen and not tell the candidate which ones they are.

The UK Civil Service currently does exactly this conceptually: candidates encounter trial items that do not affect their score, and the responses are used to calibrate future questions. citeturn19search0 LSAC likewise includes unscored questions to evaluate items for future use. citeturn19search8

This solves an important chicken-and-egg problem. You cannot know whether a question works well until real candidates answer it, yet you should not let an unvalidated new item decide someone's employment outcome.

Over time, your bank can therefore replenish itself:

> draft 10 → internal review leaves 7 → small pilot leaves 5 → live unscored data establishes 3–4 as good production items.

### Do not reuse one fixed test

The retesting literature provides a strong reason not to leave the same form online indefinitely. A meta-analysis found an average cognitive-test retest gain of 0.26 standard deviations, with larger effects when the same form was repeated and when coaching was involved. citeturn17search6

I would therefore use overlapping forms with calibrated anchor items rather than one famous “Xenon test.”

A mature architecture could look like:

**Core anchors:** a limited number of well-understood items used to link forms.

**Rotating production pool:** the majority of scored questions.

**Experimental pool:** new unscored questions.

**Retirement pool:** exposed, overused or statistically weak questions.

Do not simply generate dozens of numerical variants and assume they are equivalent. Changing a number, graph or constraint can materially change difficulty. Variants need their own empirical monitoring.

### Search-proof is necessary but no longer sufficient

Telegram's 2021 criterion was essentially “Google-proof.” citeturn23view0 In 2026, the more realistic threat model includes generative AI.

Trying to create an online multiple-choice test that advanced AI can **never** solve is probably the wrong objective. Instead, protect the integrity of the signal through the selection architecture.

For an **unaided reasoning screen**, explicitly prohibit outside assistance, draw questions from a proprietary rotating pool, and then verify high-scoring candidates with one or two fresh reasoning problems later in a live structured interaction.

Then, separately, consider a **tool-enabled work sample** where AI and normal work tools are allowed. This gives you two different signals:

> Can this person reason independently?

and

> Can this person produce exceptional work with modern tools?

Mixing those into one hidden construct will make the results harder to interpret.

I would especially avoid treating automated “AI detection” as proof of cheating. Instead, use consistency across independently administered stages as your strongest verification mechanism.


## Validation, global fairness, and rollout plan

A Telegram-like culture may admire tests that are extraordinarily difficult. A professionally defensible hiring system needs an additional question:

> **Does performance on this test actually tell us something useful about the performance we care about?**

SIOP's selection principles emphasize validation of selection procedures for their intended purpose. citeturn17search0 The U.S. EEOC's Uniform Guidelines similarly focus on job relatedness and validity where selection procedures produce adverse impact; the Guidelines' commonly cited four-fifths rule treats a group selection rate below 80% of the highest group's rate as a rule-of-thumb indicator warranting attention, although the rule is not itself a definitive legal finding. citeturn17search2

This matters because the temptation when adopting a Telegram-like strategy is to optimize for **selectivity**:

> “Only 5% passed; therefore it must be a great test.”

That is not the right metric.

A great screen is one where candidates who perform better are, to a useful degree, more likely to perform better at the next stage and eventually in the job.

### Start with job analysis

Before finalizing the blueprint, interview roughly 8–15 of your strongest performers and their managers and collect concrete examples of decisions where unusually good reasoning mattered.

Do not ask merely, “What traits do great people have?”

Ask:

> What problem did they face?

> What information did they initially receive?

> What was misleading?

> What constraint did weaker people miss?

> What did the excellent person notice?

> What did they do next?

> What changed later?

> What would a merely competent person have done?

Those stories become the substrate for item templates.

The names, numbers and proprietary facts should be fictionalized, but the **reasoning topology** can remain.

### Pilot before using a hard cutoff

Run the initial assessment first on a developmental sample: employees, contractors, recent strong/weak candidates where permitted, or applicants for whom the experimental score does not control the outcome.

For every item, monitor at least:

**difficulty:** how frequently candidates answer correctly;

**discrimination:** whether stronger overall candidates are more likely to answer it correctly;

**response time:** whether it takes dramatically longer than intended;

**omission/time-out rate;**

**alternative-choice patterns:** whether one distractor catches almost everyone for an accidental reason;

**fairness indicators:** whether performance differences suggest a language, cultural or accessibility artifact;

**relationship with downstream outcomes.**

ETS standards explicitly call for evaluation of psychometric characteristics, pretesting and analysis of reliability and test functioning after operational administration. citeturn12view1turn12view3

Do not establish the permanent cutoff by saying, for example, “we want only the top 8%, so the 92nd percentile passes.”

Instead, ask what level of reasoning is necessary for the role, combine expert judgment with observed applicant data, and subsequently test whether the cutoff distinguishes candidates on later work samples, structured interviews and job outcomes.

### Validate against a stronger downstream assessment

I would make the selection funnel:

> **Basic eligibility → Practical Reasoning Screen → Job-specific Work Sample → Structured Interview → final decision**

That design is more consistent with the current evidence than using a generic reasoning score as the sole criterion. Sackett and colleagues' revised meta-analysis found lower validity estimates than older literature had suggested for numerous selection methods and found structured interviews at the top of the revised ranking; work samples remained useful job-specific measures. citeturn18search0turn18search11

For a small elite team, this combination is particularly attractive:

The **reasoning screen** cheaply eliminates candidates who struggle with unfamiliar problems.

The **work sample** establishes whether they can turn reasoning into role-specific output.

The **structured interview** tests how they reason interactively, how they respond to challenge and whether the original test result reproduces under fresh conditions.

This gives you redundancy without requiring a large recruiting operation.

### Design explicitly for global hiring

Telegram's own rules prohibited local knowledge and asked designers to make questions understandable regardless of where the candidate lived. citeturn23view0 OECD's international assessments and EPSO's multilingual reasoning testing demonstrate how seriously large-scale international assessments treat localization and cultural accessibility. citeturn16search1turn20search0

For your screen, I recommend:

**Keep language simpler than the reasoning.** A difficult reasoning item does not need a 300-word paragraph.

**Use fictional organizations and neutral names.** Avoid assumptions tied to one country's employment, tax, education or healthcare systems.

**Explain any uncommon concepts in the prompt.**

**Use consistent units and notation.**

**Make diagrams semantically accessible**, including a textual/table equivalent where appropriate. The UK Civil Service notes, for example, that its numerical tests provide information contained in charts and graphs in table form for accessibility. citeturn19search12

**Separate language requirements from reasoning requirements.** If excellent English is genuinely necessary in your company, measure it deliberately. If it is not, don't accidentally make sophisticated English the hidden gatekeeper.

ETS's international assessment guidance specifically recognizes that linguistic and cultural diversity create validity and fairness challenges in international testing. citeturn16search6

### Monitor adverse impact rather than assuming neutrality

A “pure merit” test can still measure unintended things.

In the U.S., EEOC guidance places responsibility on the employer for its selection procedures and requires attention to validity when procedures create legally relevant adverse impact. citeturn17search2

Therefore keep, where lawful and appropriately protected, the data needed to study:

pass rates;

score distributions;

completion rates;

drop-off rates;

accommodation usage;

language/version effects;

later-stage performance by relevant demographic groups.

The goal is not to mechanically force identical distributions. The goal is to determine whether a group difference arises from a genuinely job-relevant capability or from something irrelevant such as language complexity, inaccessible visual presentation or culturally specific knowledge.

### Be careful with algorithmic or AI scoring

If the test eventually uses AI to evaluate free-text reasoning or materially automate employment decisions, additional regulatory obligations may apply.

New York City's Local Law 144 requires covered automated employment decision tools to undergo a bias audit within one year of use, requires publication of certain audit information and imposes candidate-notice requirements. citeturn15search0

In the EU, AI systems used for certain employment purposes are classified within the AI Act's high-risk framework; following the updated implementation timetable, the Commission states that rules for AI systems used in specified high-risk areas including employment are scheduled to apply from **December 2, 2027**. citeturn15search9turn15search12

That does not mean you should avoid automation. It does mean I would initially keep the reasoning screen's scored portion **deterministic and auditable**: clearly correct answers, predefined rubrics, versioned item data and traceable scoring logic.

### A practical implementation roadmap

I would build the program in four stages.

| Stage | Main work | Exit condition |
|---|---|---|
| **Construct** | Job analysis; define 5 reasoning dimensions; write blueprint and accessibility rules | Leadership and role experts agree what the screen is supposed to measure |
| **Build** | Draft roughly 180–250 candidate items; internal/red-team review; retain approximately 120–150 strong items | Every surviving item has a specification, independent solution and review trail |
| **Calibrate** | Small pilot, then embedded unscored live items; measure difficulty, discrimination, timing and subgroup patterns | Enough stable items to assemble multiple comparable forms |
| **Validate** | Compare scores with work sample, structured interview and later job performance; continuously retire/replenish items | Evidence shows the score helps make better hiring decisions |

The bank-size figures in this roadmap are **recommended operating targets**, not published psychometric standards.

I would also institute a standing rule that every quarter the hiring team reviews:

**which items are overexposed;**

**which discriminate poorly;**

**which show unexpected group or language effects;**

**which have become searchable or publicly discussed;**

**which experimental items are ready for promotion;**

**whether the test still predicts success in subsequent stages.**

The result is a living assessment rather than an online puzzle set.

The most important design principle is therefore the one that unifies Telegram's own guidance, OECD's adaptive problem-solving framework, modern test-development standards and contemporary personnel-selection research:

> **Make the assessment difficult because the candidate must reason well—not because the candidate must know something obscure, decode a trick, read unnaturally fast, or have seen the puzzle before.**

Telegram's own published rules explicitly rejected tricks, over-specialized knowledge, copied questions, weak distractors and repetitive mechanics, while rewarding originality, testing, careful explanations and inventive question design with demonstrable value. citeturn23view0turn24view1 OECD's adaptive-problem-solving work shows how to go one step further by making the difficulty arise from interacting constraints, uncertain information and changing circumstances. citeturn16search0turn16search19

For a company trying to build a **small, globally hired, unusually high-talent team**, that is the version of the Telegram philosophy I would adopt: **a hard proprietary reasoning gate, but one engineered as seriously as a product—specified, piloted, measured, rotated and validated against actual work.**