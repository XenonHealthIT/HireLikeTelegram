# Designing a Telegram-Inspired Assessment System for a Small, Global, High-Talent Team

## Executive recommendation

Telegram's hiring model is often summarized as "extremely difficult tests + tiny team," but the primary sources show something more interesting: **Telegram does not primarily try to predict whether an engineer will be good at the job through ordinary interviews. It repeatedly gives people tasks that resemble the actual work, compares the outputs, and hires from people who demonstrate unusually strong performance.** Pavel Durov describes the coding contests as a way for anyone to demonstrate skill, says Telegram may repeat contests when it wants more evidence, and gives the example of a candidate whose performance across many contests established a convincing record. He explicitly calls the contests the closest experience to what working at Telegram is like. citeturn21view0

More recently, Durov has gone even further, describing Telegram's contests as offering prize money and being "the only path" to its engineering team. Telegram's contest platform remains active and covers Android, iOS, JavaScript, machine learning, blockchain, design, art, and other domains. citeturn23search0turn21view3

There is also a lesser-known second part of the Telegram system: **general aptitude assessment**. Telegram's official 2021 aptitude-test specification says its sample tests were inspired by assessments on which Telegram staff are required to score highly. Those tests covered English communication, mathematical ability, and spatial/logical reasoning, with strong emphasis on original, culture-neutral, "Google-proof" questions rather than trivia. citeturn20view1

My recommendation is **not to copy Telegram literally**. Instead, copy its underlying principles and combine them with better-supported modern selection practices:

> **Open global entry → short job-relevant reasoning screen → difficult realistic work sample → feedback/change round → structured technical defense → optional paid trial for the final few candidates.**

The crucial difference is that the difficult part should be **difficult because the work is difficult**, not because questions are obscure, tricky, or artificially puzzle-like. Telegram itself explicitly bans riddles and trick questions from its aptitude-test design. citeturn20view1

For a small company where every hire matters disproportionately, I would optimize for **very low false-positive hiring**, while preserving multiple opportunities for exceptional candidates with unconventional résumés to prove themselves. This is compatible with Telegram's philosophy, but a work sample should be paired with a structured interview rather than treated as a perfect predictor: a major 2022 re-analysis of personnel-selection research found that many historical validity estimates were overstated and that structured interviews emerged as the highest-ranked selection procedure; separate meta-analysis shows work samples do predict job performance, but their validity is meaningful rather than magical. citeturn19search1turn19search4turn18search0

The system I would build is:


| Stage                   | Candidate burden       | Purpose                                              | Decision       |
| ----------------------- | ---------------------- | ---------------------------------------------------- | -------------- |
| Eligibility/application | 5–10 min               | Basic requirements only; no prestige filtering       | Gate           |
| Core assessment         | 45–60 min              | Reasoning, data interpretation, written clarity      | Gate           |
| Role challenge          | 3–5 hours              | Actual job performance                               | Major score    |
| Revision round          | 60–90 min              | Respond to bugs, feedback, changing requirements     | Major score    |
| Structured defense      | 60 min                 | Verify authorship, depth, judgment and communication | Major score    |
| Paid final trial        | 4–8 hours, selectively | Observe real collaboration for highest-impact hires  | Final evidence |
| Decision                | —                      | Absolute hiring bar, not quota                       | Hire / no hire |


The most important Telegram idea to preserve is this: **you are allowed to hire nobody**. A difficult assessment ceases to mean much if the organization feels compelled to select the top candidate regardless of the quality of the field.

## What Telegram actually does



### It uses open competitions instead of relying on pedigree

Durov's description of the system is unusually explicit. Anyone can participate in a coding competition, including people primarily interested in the prize rather than a job. Telegram observes the resulting work and selects strong performers. When one result does not provide enough evidence, Durov says they can run another task and obtain more data. He cites repeated success across different technologies as especially compelling evidence. citeturn21view0

That has a major implication for your company's design: **the résumé should be used mainly for eligibility and contextual information, not as the primary measure of talent**. Telegram's model creates a route for a talented person without a famous employer, degree, or professional network to beat somebody with a more conventional pedigree by producing better work. This follows directly from the open-contest model Durov describes. citeturn21view0

This is especially compatible with global hiring. Telegram's developer platform states that everybody can inspect submissions and report issues, while contestants are represented under animal aliases during testing "to ensure fairness and transparency." Telegram administrators also independently check submissions and calculate results. citeturn21view3

That suggests three useful design principles for your company:

**First, anonymize work-sample evaluation where feasible.** Reviewers should initially see candidate IDs, not school, nationality, previous employer, gender, or photograph.

**Second, separate evaluation from recruiting.** The assessor should be judging an artifact against a rubric, not deciding how impressive the candidate seems.

**Third, collect more than one observation when the evidence is ambiguous.** Telegram's repeated-contest philosophy is essentially repeated measurement rather than betting everything on a single interview. citeturn21view0

### Telegram's contests look remarkably like production work

The strongest part of the Telegram approach is that challenges are often actual engineering problems rather than abstract algorithm puzzles.

In its 2025 Android competition, Telegram required candidates to implement redesigned profile screens inside the existing Telegram Android application. Contestants had to use Java, could not use third-party UI frameworks, had to preserve the performance and stability of the existing application, had to follow the supplied design and animations precisely, and were told that their code would be reviewed and tested across a wide range of Android devices. citeturn22view0

That is quite different from asking someone to solve a binary-tree problem on a whiteboard. It simultaneously reveals whether the person can:

- understand a large unfamiliar codebase;
- follow constraints;
- produce robust software;
- make sensible implementation choices;
- pay attention to visual/product details;
- avoid regressions;
- finish something usable.

Telegram's 2021 Android contest was even more open-ended: participants were asked to **proactively find and fix imperfections**—bugs, glitches, poor animations and performance problems—and were rewarded based partly on the importance and difficulty of the issues they identified and solved. citeturn17search1

Telegram's machine-learning competition used the same philosophy in another domain. Contestants had to build a library that identified the programming or markup language of arbitrary snippets. The solution had to work locally without network access, respond within 10 milliseconds for a 4,096-character input, work on a specified clean Linux environment, and was evaluated primarily for accuracy and then speed using data from public Telegram chats—including messy inputs that might not be valid code at all. citeturn21view2

These examples reveal what "difficult" means in Telegram's system: **messy, constrained, realistic and objectively testable**.

### Evaluation is more detailed than winner versus loser

Telegram also publishes unusually granular evaluation evidence. In the 2025 Android contest, it reported 90 initial entries, discarded empty or non-functional submissions, applied penalties to entries that had to be rebuilt because they failed submission requirements, and spent tens of hours reviewing applications. It ultimately published multiple prize tiers, planned detailed reviews of strong and weak points, and said some top winners would be contacted about further cooperation. citeturn22view1

This is important because the Telegram model is not simply:

> "Give impossible test → hire top score."

It is closer to:

> **Create high-fidelity task → impose meaningful constraints → inspect actual artifact → test edge cases → penalize sloppiness → compare quality → give feedback → repeat → hire when evidence becomes compelling.**

Durov himself says the contests are useful not merely because Telegram identifies good people, but because Telegram also obtains competing solutions to valuable technical problems. citeturn21view0

I would **not** copy that last aspect literally for employment candidates unless the assessment is compensated. Otherwise, a company risks turning recruiting into unpaid productive work. Telegram's public contests have prize funds; your private hiring assessment should similarly compensate finalists when tasks become substantial. Telegram's contest platform documents significant prize funds across many competitions. citeturn21view3

## What kind of questions Telegram asks

There are really **two different Telegram assessment families**, and separating them is important.

### General aptitude assessment

Telegram's official aptitude-test documentation says its sample tests were modeled on assessments that Telegram staff are required to score highly on. The specification used three categories: English Language, Mathematical Ability, and Spatial & Logical Thinking. citeturn20view1

The **English section** was supposed to test concepts useful for everyday communication rather than obscure grammatical rules. Telegram explicitly said it should not be a vocabulary or spelling test. Correct use of words in context was acceptable; memorizing definitions, synonyms or spellings was not the goal. citeturn20view1

The **mathematical section** focused on day-to-day numerical reasoning: arithmetic, graphs, ratios, percentages and basic algebra. Telegram specifically cautioned against assuming knowledge of advanced formulas unless the formula was supplied in the question. citeturn20view1

The **spatial/logical section** was divided between spatial reasoning—rotation, reflection, translation, 2D and 3D shapes—and broader logical problem solving. Telegram said logical questions could contain mathematics, but mathematics should not be the entire problem. citeturn20view1

The test-design rules are arguably more valuable than the categories. Telegram required questions to be original, resistant to simple search-engine lookup, understandable without country-specific knowledge, varied in format, and supported by plausible distractors and explanations. It explicitly prohibited riddles and trick questions. Typical timers were expected to be around one or two minutes per question, although Telegram did not mandate a single timer. citeturn20view1

For entry to the 2021 Aptitude Test Contest, Telegram published unusually high-looking combinations of scores. Candidates passed if they achieved one of these combinations: at least 26 on the score Telegram labeled **Cognitive** plus at least 16 in **Language**; at least 25 Cognitive plus 19 Language; or at least 29 Language plus 20 Cognitive. Those thresholds were for entry into this particular contest—not evidence of a current universal Telegram employee cutoff—and should not be copied blindly. citeturn17search1

The original Telegram post pointed candidates to a course containing their results, explanations and comparisons with other participants. I could not verify an authoritative, currently accessible archive containing every original question, so I would not present internet-reconstructed questions as genuine Telegram questions. What can be established strongly from the primary documentation is the **question philosophy and subject matter** above. citeturn17search1turn20view1

### Work-sample questions

The technical contests are where Telegram's hiring model becomes much more distinctive. These are not really "questions" at all; they are assignments.

Representative Telegram tasks include:


| Telegram task                                                                                                                                                              | What it actually measures                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Rebuild/redesign Android profile flows inside Telegram's existing codebase, under language/framework constraints and with exact animation requirements. citeturn22view0 | Codebase navigation, architecture, UI engineering, product quality, attention to detail, performance |
| Proactively find and fix important Android bugs, visual flaws and performance problems. citeturn17search1                                                               | Initiative, diagnosis, prioritization, debugging, craftsmanship                                      |
| Build a programming-language classifier with a strict latency ceiling, no network dependency and evaluation on real messy data. citeturn21view2                         | Algorithm design, optimization, robustness, engineering discipline                                   |
| Create a complete cross-platform product-design concept with both user/admin flows and implementation-ready thinking. citeturn22view1                                   | Product reasoning, systems thinking, visual design, completeness                                     |


Telegram also asks for evidence around the work. Its aptitude-test contest required contestants not only to create three 30-question assessments, but also to submit a cover letter explaining their design reasoning, review other contestants' submissions, and later submit a rebuttal addressing criticism of their own work. citeturn20view1

That is a particularly good idea for a small-team company. A high-performing employee must often be able to do four things:

> **produce → explain → critique → respond to critique.**

I would explicitly test all four.

## What research says to copy — and what not to copy

Telegram's most defensible idea is the **high-fidelity work sample**. A meta-analysis of work-sample tests found an observed average correlation of .26 with job performance, rising to .33 after correction for unreliability in the performance criterion. The same research also cautioned that earlier literature had overstated work-sample validity, so work samples should be treated as useful evidence, not infallible truth. citeturn18search0

That caution matters. A hiring system consisting exclusively of one massive contest may reject excellent employees who happen to perform badly once or disproportionately reward people who have extraordinary amounts of free time to devote to the contest.

There is strong justification for pairing the work sample with a **structured interview**. Sackett and colleagues' major 2022 reassessment of selection research concluded that historical validity estimates for many selection tools had been overcorrected, but structured interviews remained especially strong and became the top-ranked selection procedure in their revised comparisons. citeturn19search1turn19search4 A newer meta-analysis covering 37 studies and more than 30,000 participants found interview assessments related to later task and contextual performance, with evidence that more structured question-by-question scoring can improve some evaluations. citeturn18search3turn18search6

So, scientifically, I would modify the pure Telegram model into:

**work sample + structured defense + repeated evidence.**

That combination is particularly appropriate for a tiny team because the work sample tests whether somebody **can do** the work while the structured interview can probe whether they understand their decisions, communicate well, respond to ambiguity and exhibit the behaviors required when working with a very small number of colleagues.

There is another useful comparison. Automattic—another company known for distributed work—currently describes a hiring process that can include a skills/criteria assessment, interview and **paid trial consisting of a role-aligned project or tasks**, followed in many cases by a final interview. citeturn17search10 A hybrid of Telegram's competitive work sample and Automattic's compensated trial is, in my view, better suited to normal company hiring than copying Telegram's weeks-long public competitions literally.

### Where I would deliberately depart from Telegram

I would **not use a generic IQ-style test as the dominant hiring gate**. Telegram's aptitude design is interesting, but U.S. EEOC guidance stresses that employment tests should be properly validated for the position and purpose for which they are used, should be job-related, and should be reconsidered when a similarly effective alternative has less adverse impact. citeturn17search5

The Uniform Guidelines use the four-fifths or 80% selection-rate rule as one rule of thumb for identifying potentially substantial group differences, although the legal analysis is more nuanced than that single statistic. citeturn17search9

Therefore:

**Do not test spatial rotation for a backend engineer merely because Telegram does.** Test it only where it has a defensible connection with the work.

**Do not make English sophistication a proxy for intelligence.** If your working language is English, assess the ability to understand requirements and communicate clearly—the same practical emphasis Telegram specifies—rather than accent, obscure vocabulary or idioms. citeturn20view1

**Do not maximize time pressure for its own sake.** A time constraint should represent prioritization or actual job demands, not simply manufacture failure.

**Do not use trick questions.** Even Telegram explicitly rejects them. citeturn20view1

**Do not set a difficulty target such as "only 1% may pass."** Set a capability standard first, then observe the pass rate. A 2% pass rate is meaningful only if that 2% genuinely meets a job-relevant bar.

For U.S. hiring in particular, selection procedures that disproportionately exclude protected groups can create legal issues if they cannot be justified as job-related and consistent with business necessity; the EEOC recommends monitoring selection procedures and considering comparably effective alternatives with less adverse impact. citeturn17search2turn17search5 A global system will additionally require jurisdiction-specific review rather than assuming one set of rules applies worldwide.

## Recommended assessment architecture

I would implement a **Telegram-inspired talent tournament**, but make it much shorter, standardized and explicitly connected to job performance.

### Open global entry

Do not begin by asking "Which university?" or "Which famous company?"

Begin with:

> Are you legally/operationally eligible for this role?  
> Can you work under the required collaboration conditions?  
> Can you demonstrate the skills?

Allow candidates from anywhere your employment infrastructure permits. The first substantial judgment of quality should come from the assessment, not pedigree.

For hard-to-fill technical roles, you can eventually operate two entry routes:

**Continuous hiring:** candidates apply at any time and complete the standardized assessment.

**Periodic challenge:** run a Telegram-style public challenge quarterly or twice per year, pay prizes, publish interesting results where confidentiality permits, and invite consistently strong performers into the hiring process.

The second route creates a long-term talent community instead of restarting sourcing from zero every time you need someone. This most closely captures Durov's repeated-evidence model. citeturn21view0

### Core assessment

Target **45–60 minutes**, rather than Telegram's much more extensive aptitude framework.

For most knowledge-work roles, I would use approximately:


| Construct                   | Approximate weight | Example                                                                       |
| --------------------------- | ------------------ | ----------------------------------------------------------------------------- |
| Logical problem solving     | 30%                | Resolve constraints, identify implications, diagnose inconsistent information |
| Quantitative/data reasoning | 25%                | Interpret graphs, rates, percentages, capacity and uncertainty                |
| Written comprehension       | 20%                | Extract requirements from dense but realistic material                        |
| Written communication       | 15%                | Select or produce a clear, concise explanation                                |
| Role-specific mini-items    | 10%                | Code reading, product judgment, analytical reasoning, etc.                    |


I would **not** include a spatial section by default. Add it only to roles where spatial reasoning genuinely represents relevant work.

The Telegram principles worth retaining are: make questions original and difficult to solve by simple searching; avoid cultural trivia; keep distractors plausible; avoid riddles; and require question authors to document why an item has one defensible answer. citeturn20view1

This stage should be a **minimum-capability gate**, not the dominant final score. Its purpose is to reduce a global applicant pool efficiently enough that you can afford to inspect substantive work.

### Role challenge

This should be the center of the system.

Give candidates a **three-to-five-hour timebox** inside a broader scheduling window. The challenge should look like work they might encounter three months after joining the company, but use synthetic, open-source or deliberately isolated material rather than productive proprietary work.

For software engineering, for example:

> "Here is an unfamiliar repository and a feature request. Implement the feature while retaining backward compatibility. A visible test suite covers normal cases; additional hidden tests cover edge cases. You have a latency budget and may not introduce more than one new dependency. Include a short design note explaining important tradeoffs."

That reproduces many Telegram characteristics: unfamiliar existing system, functional requirements, technical constraints, performance considerations, objective testing and an explanation of reasoning. citeturn22view0turn21view2

A good software rubric might be:


| Dimension                       | Weight |
| ------------------------------- | ------ |
| Functional correctness          | 25%    |
| Robustness and edge cases       | 20%    |
| Architecture/code quality       | 15%    |
| Performance/resource discipline | 10%    |
| Product judgment                | 10%    |
| Testing discipline              | 10%    |
| Explanation and tradeoffs       | 10%    |


Crucially, define **critical failures** independently of the numerical score. Examples could include a major security vulnerability, inability to run the submission, fabricated results, destructive data handling, or complete violation of a core requirement.

That prevents someone from accumulating enough style points to compensate for something that would be unacceptable in production.

### Feedback and revision round

This is the stage I think would make your system unusually powerful.

After the original submission, automatically or manually provide three pieces of feedback:

> "This breaks when X occurs."  
> "The requirement has now changed from A to B."  
> "Your implementation passes normal load but misses the new latency target."

Give the candidate another **60–90 minutes**.

Now evaluate:

- whether they correctly understand feedback;
- how quickly they isolate the issue;
- whether the fix creates regressions;
- whether they defend a reasonable decision instead of blindly obeying incorrect feedback;
- how clearly they communicate what changed.

Telegram's repeated rounds and Durov's emphasis on gathering more evidence point in this direction, while Telegram's aptitude contest also explicitly assessed peer review and rebuttal. citeturn21view0turn20view1

This stage can distinguish two candidates whose initial solutions both looked excellent. In a tiny team, **rate of improvement after feedback** may be almost as important as first-attempt brilliance.

### Structured defense

Every finalist gets the same core interview structure.

Do not make it an informal "chat with the founder."

For engineering, I would ask approximately:

**Artifact defense:**  
"Walk us through the hardest decision you made. What alternatives did you reject and why?"

**Failure analysis:**  
"What part of your submission are you least confident about?"

**Requirement change:**  
"If traffic increases tenfold, what fails first?"

**Debugging:**  
"Here is one hidden test your solution failed. Diagnose it."

**Ownership:**  
"You notice a serious unrelated problem in this repository while working on your task. What do you do?"

**Collaboration:**  
"A colleague strongly disagrees with your architecture and their argument is partly correct. Show us how you would resolve it."

**Learning:**  
"What did you learn during this challenge that would change your solution if you restarted?"

Every interviewer should have behavioral anchors before the conversation starts. For example:

> **Score 1:** cannot explain choice; becomes inconsistent under probing.  
> **Score 3:** explains implementation and obvious tradeoffs accurately.  
> **Score 5:** identifies non-obvious tradeoffs, limitations and alternatives; updates reasoning appropriately when given new evidence.

Have two assessors score independently **before discussing the candidate**. That preserves considerably more information than reaching an intuitive consensus in real time, and the research literature favors structured scoring over unstructured impressions. citeturn18search6turn19search4

### Paid final trial

For especially consequential roles, reduce your uncertainty one more time.

Take the best two or three candidates and conduct a **paid half-day or one-day collaboration exercise**. Automattic's current hiring model demonstrates the viability of using a paid, role-aligned trial in a distributed-company hiring process. citeturn17search10

The candidate might receive a small project, interact asynchronously with two future colleagues, receive a review, make a change and produce a final handoff.

This is where you observe something the solo contest cannot fully reveal:

> **Does this exceptional individual make the small team better to work in?**

Do not convert this into weeks of speculative free labor. The more closely a hiring task resembles commercially valuable work and the more candidate time you consume, the stronger the case for compensation.

## A concrete Telegram-inspired question bank

The following are **original examples I would recommend for your system, not leaked or verbatim Telegram questions**. They deliberately follow Telegram's documented preference for practical communication, quantitative reasoning, problem solving, originality and search resistance. citeturn20view1

### Written communication

**Prompt**

An engineer posts:

> "We fixed the payments issue. It seems like the database got overloaded maybe because there were more retries than usual but we changed some stuff and it looks okay now. We should probably monitor it."

Ask the candidate to select the best status update from four alternatives.

The best alternative should identify **what happened, customer impact, what was changed, current status and next action**, without adding unsupported certainty.

This tests clarity rather than vocabulary.

### Quantitative reasoning

**Prompt**

A service handles 2,400 requests per minute at 60% CPU usage. A new feature increases CPU consumption per request by 25%. Assume everything else remains linear.

Ask:

> Approximately what CPU utilization would you expect at the original request rate?

Answer: 60 \times 1.25 = 75.

Then make the real question harder:

> Traffic is projected to increase by another 20%. Does the existing capacity remain acceptable under an 85% operating limit?

Expected utilization becomes 75 \times 1.2 = 90, so no.

That tests percentages and multi-step reasoning in a job-relevant context—the kind of basic quantitative skill emphasized in Telegram's specification. citeturn20view1

### Constraint reasoning

**Prompt**

Four deployments—A, B, C and D—must be completed.

A must happen before C.  
B and D cannot occur simultaneously.  
C requires engineers Mia and Chen.  
D requires Chen.  
Only two deployment windows remain.

Present four proposed schedules and ask which one is feasible.

This measures logical constraints without relying on culturally specific knowledge or a puzzle "gotcha."

### Requirement comprehension

Provide a one-page synthetic feature specification containing:

- three mandatory requirements;
- two optional behaviors;
- one contradiction;
- one unspecified edge case.

Ask the candidate:

> "Which three questions would you ask before implementation?"

A mediocre candidate asks generic questions. A strong candidate identifies the ambiguity that could materially alter the architecture.

### Engineering work sample

Give a repository containing:

- an incomplete feature;
- one obvious bug;
- one non-obvious race condition or edge case;
- visible unit tests;
- hidden tests;
- a performance constraint.

Ask the candidate to implement the feature and provide a 300-word engineering note.

Do **not** award maximum scores simply for passing the tests. Hidden-test correctness, simplicity and judgment should all matter.

This resembles Telegram's real competitions substantially more than ordinary algorithm trivia. citeturn22view0turn21view2

### Debugging and ownership

Tell the candidate:

> "While implementing the requested feature, you discover an unrelated bug that can silently corrupt approximately 0.1% of records. Fixing it completely would cause you to miss today's feature deadline."

Ask for:

1. the immediate action;
2. what they communicate;
3. what they would change in the code;
4. what they deliberately would **not** do.

There is intentionally no single-line mathematical answer. The rubric should reward risk recognition, containment, escalation, documentation and proportionate action.

### Revision challenge

After the candidate submits:

> "Production profiling shows that your solution's p99 latency is 180 ms. The requirement is 100 ms. You have 75 minutes. You may alter the implementation but not the API."

This tests precisely the kind of performance discipline visible in Telegram's competitions, where technical constraints can be explicit and objective. citeturn21view2

### Product or design challenge

For a product or design hire:

> "Design an account-switching workflow for a product in which a user may belong to personal, company and client workspaces. Produce the primary flow, permissions model, error states and a short rationale. After submission, you will receive an additional admin requirement and must revise your design."

This mirrors the broad character—not the content—of Telegram's design competitions, which require complete product concepts, implementation-aware thinking, multiple user perspectives and deliverable artifacts. citeturn22view1

## Scoring, AI, fairness, and rollout



### Use an absolute bar, not simply "top candidate wins"

Before candidates take the assessment, have several of your own strongest employees complete it independently under equivalent conditions.

Use those results to answer:

- Which parts actually distinguish stronger performers?
- Which requirements are unnecessarily ambiguous?
- How much time is genuinely required?
- What does "excellent" look like?
- Which mistakes should be disqualifying?

Then define your minimum bar **before looking at candidate identities**.

For example:

> Work sample: at least 75/100  
> No critical failure  
> Correctness: at least 18/25  
> Robustness: at least 14/20  
> Structured defense: at least 4/5 on technical depth  
> Overall weighted score: at least 80/100

The numbers above are starting design parameters, not scientifically validated thresholds. Your pilot data should determine the real cut scores.

Most importantly:

> **Candidate A scoring 81 should be hired even if someone else scores 95. Candidate B scoring 74 should not be hired merely because 74 is the highest score this month.**

That is how you preserve a small-team talent bar.

### Blind the artifact, not the entire process

Telegram uses animal aliases on its contest platform during testing. citeturn21view3

You can borrow that elegantly:

**Initial artifact review:** Candidate XQ-417.  
**Reviewer sees:** submission, tests, explanation.  
**Reviewer does not see:** name, university, nationality, photograph, previous employers.

After the artifact has been independently scored, reveal the candidate for the structured interview.

This gives you the benefits of contextual information later without allowing pedigree to contaminate the first technical-quality judgment.

### Design for AI rather than pretending it does not exist

A particularly interesting current signal is that Durov recently praised contest winners, describing some of them as using "AI sidekicks," while simultaneously reiterating that contests are the route into Telegram's engineering team. citeturn23search0

A Telegram-inspired assessment in 2026 therefore should not depend on the assumption that candidates cannot access AI.

I would use this policy:

**Take-home/work sample:** AI tools allowed. State exactly what is permissible. Require the candidate to take responsibility for every submitted line and decision.

**Structured defense:** candidate must explain the solution in depth and make a small modification under observation.

**Revision round:** give a previously unseen requirement and observe how they adapt.

That makes authorship fraud much less useful. Someone can outsource the initial solution, but they still have to understand, defend, debug and modify it.

More fundamentally, if your employees will use AI at work, the most valid question increasingly becomes:

> **"How good is the work this person can reliably produce with the tools we permit?"**

rather than:

> "How good are they at pretending those tools do not exist?"



### Protect global accessibility

One Telegram rule is especially worth copying exactly in spirit: questions should not require local cultural knowledge. Telegram's aptitude specification even recommends standardized conventions such as metric units where possible. citeturn20view1

For a global test, I would additionally avoid:

- sports trivia;
- local tax or legal assumptions unless role-relevant;
- American idioms;
- unnecessarily complex English;
- ambiguous date formats;
- currency conversions unrelated to the competency;
- questions whose difficulty mainly comes from being a non-native English speaker.

I would *depart* from Telegram's 2021 same-time global assessment. Telegram scheduled everybody simultaneously to create a level playing field. citeturn20view1 For normal global hiring, I would instead offer multiple equivalent forms or controlled assessment windows so geography and time zone do not become irrelevant selection criteria.

### Monitor whether the test actually works

Do not declare the assessment "validated" because senior engineers like the questions.

Track, by assessment version and role:

**Assessment metrics:** item difficulty, item discrimination, abandonment rate, time per item, stage conversion and reviewer disagreement.

**Hiring metrics:** offer rate, acceptance rate, candidate time burden and cost per successful hire.

**Outcome metrics:** manager ratings, objective quality metrics where available, ramp time, retained performance at six and twelve months.

Then test whether the hiring scores actually predict those outcomes.

This is particularly important because the personnel-selection literature warns against assuming very high predictive validity from any single procedure. citeturn19search1turn18search0

Where lawful to collect the necessary information, also examine differences in selection rates across groups. In the United States, the EEOC specifically recommends ensuring that tests remain appropriate to the job, monitoring changes in job requirements, and considering effective alternatives when a procedure disproportionately screens out a protected group. citeturn17search5turn17search9

### Roll it out as an experiment rather than a company-wide revolution

For the first hiring cohort, I would choose **one role with frequent enough recruiting volume**, ideally software engineering.

Build approximately 60–100 core items so multiple equivalent test forms can be created, but expose only a subset to any candidate. Build three interchangeable role challenges around the same competency model to reduce answer leakage.

Have ten or more strong incumbents complete the test before launch. Record their scores and, more importantly, their criticism of each item.

During the first real cohort, I would initially let a slightly wider group reach the work sample than you ultimately expect to. That gives you data about whether the core screen is accidentally eliminating people who subsequently perform extremely well.

After roughly the first 30–50 serious candidates, inspect false negatives and false positives qualitatively. After several hiring cohorts, begin criterion-validation analysis against actual job performance rather than continuously moving the bar based on intuition.

The assessment should then become a **product that your company maintains**, not a document HR writes once. Telegram continuously runs new contests, changes the challenge according to the work, gathers feedback on submissions and uses repeated performance as evidence. citeturn21view0turn21view3

The mature version of your system should therefore look approximately like this:

> **Global, pedigree-light entry**  
> ↓  
> **45–60 minute practical reasoning screen**  
> ↓  
> **3–5 hour realistic role challenge**  
> ↓  
> **blind scoring + hidden tests**  
> ↓  
> **feedback/change round**  
> ↓  
> **structured artifact defense**  
> ↓  
> **paid collaboration trial for the final few**  
> ↓  
> **absolute quality bar — including the option to hire nobody**

That captures what is most powerful about Telegram's model without copying its weaknesses. Telegram's distinctive insight is not simply that the test should be exceptionally hard. It is that **a small organization should accumulate direct evidence that a candidate can produce exceptional work before giving that person the leverage that comes with joining a tiny, high-performing team**. Durov's repeated-contest philosophy captures that explicitly; modern selection research supports adding structured interviewing and careful validation around it. citeturn21view0turn19search4turn18search6