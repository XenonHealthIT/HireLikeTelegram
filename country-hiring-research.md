# Remote Engineering Hiring: Country Research

> [!CAUTION]
> **⚖️ This document is not legal advice. Legal counsel must review any hiring decision before we act on it.**
>
> The engineering team compiled this from public sources as a first-pass country shortlist. Lawyers and HR **must confirm** the following before we act:
> - The independent-contractor agreement template, and the risk that a contractor is reclassified as an employee in each country
> - The clause making contractors solely responsible for local tax and labor reporting, and how far it actually protects us
> - Tax and permanent establishment (PE) risk
> - IP assignment terms
> - Cross-border transfer of patient data and personal data
> - The US sanctions (OFAC) screening process
>
> Regulations change fast. The content reflects the research date.

> Research date: 2026-10-15 (updated 2026-10-19)
> Scope: a US company engaging remote backend/data engineers as **independent contractors**. Time zones are not a factor.
> Ranking principle: **contractor policy first** (how safe and simple it is to engage contractors, reclassification risk, regulatory stability, payments). Talent, English, and cost come second.
> Salary figures come mostly from recruiting vendors. Read them as orders of magnitude, not exact numbers.

## Engagement model

**Management decision:** all hires are onboarded as **independent contractors** and are **solely responsible for local reporting to tax and labor authorities**. Poland and Ukraine are excluded.

What this means in practice:
- **US side:** a foreign contractor working entirely outside the US provides **Form W-8BEN** (or **W-8BEN-E** for a company).
- **Local side:** a contract label alone does not decide status. In every shortlisted country, authorities and courts look at the **actual working relationship**. If a contractor works like an employee (full-time, fixed hours, managed by us, working only for us), they or the local authorities can still claim employment rights and back contributions. The reporting clause shifts the *filing* duty to the contractor, but it does not fully remove that risk.

To keep the contractor model defensible (for legal to confirm):
1. **Contract with the engineer's own registered business** where possible, for example a Bulgarian EOOD, an Indian sole proprietorship with GST registration, or a Romanian PFA or SRL.
2. **Use deliverable-based statements of work (SOWs)**, with no required working hours.
3. Contractors **use their own equipment** and are **free to take other clients**.
4. Pay **against invoices**, not as a salary.
5. Include a **written IP assignment** in every agreement (see each country below).

## Executive summary

| # | Country | Why | Contractor setup | Senior rate (approx./yr) |
|---|---|---|---|---|
| 1 | 🇧🇬 **Bulgaria** | EU and euro (since 2026), 10% flat tax; IOI 2025: 2 golds and 2 silvers | Freelancer, sole trader, or **the engineer's own EOOD company (lowest risk)** | $62–96k |
| 2 | 🇮🇳 **India** | Largest talent pool; contractor model very common and well understood | Sole proprietor with GST registration; exported services at 0% GST | $40–70k+ |
| 3 | 🇷🇴 **Romania** | Best algorithmic talent (IOI 2025: 4 golds); English #11 worldwide | PFA (sole practitioner) or micro-SRL; **must meet 4 of 7 independence criteria** | $65–104k |

**Sourcing:** our process already works like a contest, so contests are the best channel for reaching strong engineers. See *Recommended next steps*.

### Points that apply to every country
- **IP must be assigned in writing.** Work a contractor creates does not belong to the client by default.
- **Patient data:** each country has its own cross-border rules (GDPR in Bulgaria and Romania, the DPDP Act in India). The simplest approach is to give contractors only de-identified or synthetic data.
- **Permanent establishment risk:** contractors should never negotiate or sign contracts on our behalf.
- **Sanctions screening:** screen every contractor against the OFAC SDN list and verify where they actually live.
- **Competitive pay:** to win top talent, expect to pay around the 75th–90th percentile of the local market.

---

## 1. 🇧🇬 Bulgaria

**Why**
- 2 golds and 2 silvers at IOI 2025, unofficially 4th as a team (ahead of the USA) and Bulgaria's best result ever.
- English is #18 worldwide on EF EPI.
- **Joined the eurozone on 1 Jan 2026.** Contractors invoice in EUR over SEPA, with no currency controls.
- **Risks:** a smaller pool (about 60k software professionals) and political volatility. The 2026 budget did not pass, and early elections were held in April 2026, so tax rules can change at short notice.

**Contractor policy**
- **Forms used in IT** (all common):
  - A freelancer on a civil contract pays about 7.5% effective tax (10% tax on income after a 25% statutory expense deduction).
  - A sole trader (ET) is also an option.
  - A one-person company (EOOD) pays 10% corporate tax plus 5% on dividends.
- **Reclassification:**
  - The Labour Inspectorate can declare an employment relationship under Labour Code art. 405a.
  - The tests are subordination, fixed hours, working only for one client, client-supplied tools, and salary-like payments.
  - The tax agency collects back contributions.
  - A foreign client with no Bulgarian entity has limited practical exposure. **Contracting with the engineer's own EOOD lowers the risk further.**
- **If reclassified as employment:** employer contributions of about 19% (capped), at least 20 days of paid leave, notice of 30 days or more, and about 1 month's severance for redundancy.
- **IP:** the statute that gives employers ownership of employee-written software does not cover contractors. A **written assignment** must cover territory, term, and all uses.
- **Data:** GDPR applies (regulator: the Commission for Personal Data Protection). Transfers to the US need the EU-US Data Privacy Framework or Standard Contractual Clauses.

**Rates (USD per year)**

| Level | Local market | Remote contractor for a foreign company |
|---|---|---|
| Junior | $18–32k | — |
| Mid | $29–57k | ~$48–66k ($23–32/hr) |
| Senior | $43–99k | ~$62–96k ($35–46/hr) |

**Platforms:** **DEV.BG** (the leading IT board, with an international employer portal), jobs.bg, and LinkedIn. For algorithmic talent: national olympiad and IOI alumni, and the Sofia and Varna mathematics high schools.

---

## 2. 🇮🇳 India

**Why**
- About 5.8M tech workers, with English as the working language.
- The largest Codeforces and CodeChef population. Our rigorous testing makes high applicant volume an advantage.
- **Risks:** quality varies a lot between IT-services and product-company backgrounds, many people serve 60–90 day notice periods, counter-offers are common, and attrition is high.

**Contractor policy**
- **Common and well understood.** Many Indian engineers already invoice foreign clients.
- **GST:**
  - Exported services carry 0% GST if the contractor files a Letter of Undertaking (LUT).
  - Registration is required above ₹20 lakh turnover.
- **Payments:**
  - The contractor's bank issues a foreign-remittance certificate (FIRC/FIRA).
  - A US payer with no Indian presence has no Indian withholding (TDS) obligation.
- **Reclassification:** depends on how much control we exercise and how integrated the contractor is. Exclusivity, fixed hours, and company equipment all raise the risk.
- **If reclassified as employment:** the new Labour Codes (in force since 21 Nov 2025) bring provident fund at 12%, gratuity of about 4.81%, and dismissal protections for non-supervisory "workers".
- **PE risk:** India has rejected the OECD's 2025 home-office safe harbour. Keep contractors out of sales and contract negotiation.
- **IP:** a contractor assignment must say **"worldwide, perpetual"**. Otherwise it defaults to 5 years and India only.
- **Data:** the DPDP Rules phase in fully by May 2027. US patient data remains governed by HIPAA.

**Rates (USD per year, product-company level)**

| Level | USD per year | Contractor hourly rate |
|---|---|---|
| Junior | $9–23k | — |
| Mid | $14–40k | $20–45/hr |
| Senior | $40–70k+ | $30–72/hr |

**Platforms:** **Naukri** (largest, but noisy), LinkedIn, Instahyre, Cutshort, Wellfound. For algorithmic talent: CodeChef, Codeforces, ICPC regionalists, and IIT/NIT/BITS alumni.

---

## 3. 🇷🇴 Romania

**Why**
- 4 golds at IOI 2025, Romania's best result ever.
- English is #11 worldwide on EF EPI.
- About 205k IT employees in 2025. A wave of layoffs in 2026 has increased the number of available candidates.
- **Risk:** taxes change often. They rose through 2025–26, and contractor and micro-company rules are tightening.

**Contractor policy**
- **Forms used in IT** (very common):
  - A PFA (sole practitioner) pays 25% pension and 10% health contributions on a minimum base.
  - A micro-SRL company was taxed at 1% for 2026, but only with revenue under €100k and at least one employee. The regime may be abolished in 2027 (unverified).
- **Reclassification:**
  - Fiscal Code art. 7 requires at least **4 of 7 independence criteria**, for example freedom over how and when to work, multiple clients, own equipment, and own business risk.
  - **Working full-time and only for one client is high risk.** Romania is the strictest of the three on this point.
- **If reclassified as employment:** low employer cost (about 2.25%) but back contributions, at least 20 days of leave, and notice of 20 working days.
- **IP:** contractors need a **written assignment**. Moral rights cannot be transferred.
- **Data:** GDPR applies. Transfers to the US need the EU-US Data Privacy Framework or Standard Contractual Clauses.

**Rates (USD per year)**

| Level | Employment-equivalent (gross) |
|---|---|
| Junior | $26–35k |
| Mid | $42–61k |
| Senior | $65–104k |

- Contractor rates for seniors run about $45–90/hr (vendor data, wide spread).
- Contractors typically charge 20–40% above the gross salary equivalent.

**Platforms:** LinkedIn (main channel), eJobs, BestJobs, and devjob.ro. For algorithmic talent: olympiad alumni, infoarena, Kilonova, and pbinfo.

---

## Recommended next steps

1. **First cohort:** open contractor roles in **Bulgaria, India, and Romania**. Then compare talent quality using real R0–R2 pass rates and scores.
2. **Source through contests.**
   - Our process already works like a contest, and contest channels attract the strongest algorithmic engineers.
   - One option is to sponsor a Codeforces round. Each round draws about 15–25k registrants and reaches India and Eastern Europe at once.
   - Another is to follow Telegram's model and run our own prize contest that feeds directly into R0.
   - Details are in [sourcing-platforms.md](sourcing-platforms.md).
3. **Legal:** prepare one **independent-contractor agreement template** with country riders for Bulgaria, India, and Romania. It should cover:
   - deliverable-based SOWs
   - the contractor's responsibility for local tax and labor reporting
   - a worldwide, perpetual IP assignment
   - confidentiality and data-handling rules
   - a sanctions representation
4. **Finance:** set up contractor payments (W-8BEN collection, invoice-based payment via bank wire or a contractor payment platform).

---

## Key sources
- **Bulgaria:** [PwC contributions](https://taxsummaries.pwc.com/bulgaria/individual/other-taxes), [IOI 2025 (BAS IMI)](https://math.bas.bg/two-gold-and-two-silver-medals-from-the-international-olympiad-in-informatics-in-bolivia/?lang=en), [EF EPI](https://www.ef.edu/epi/regions/europe/bulgaria), [Eurozone entry (BTA)](https://www.bta.bg/en/news/926015-bulgaria-clears-last-hurdle-to-eurozone-entry-on-january-1-2026), [Sector data (BTA)](https://www.bta.bg/en/news/1024306-software-sector-in-bulgaria-reports-11-5-revenue-growth-in-2024), [Art. 405a reclassification](https://www.innovires.com/en/blog/skrit-trudov-dogovor-prekvalifikacia-kt-405a.html), [IP (Eurofast)](https://eurofast.eu/understanding-intellectual-property-rights-in-bulgarian-employment/), [Lemon.io rates](https://lemon.io/rate-calculator/bulgaria/)
- **India:** [AZB Labour Codes](https://www.azbpartners.com/bank/india-implements-new-labour-codes-an-overview-into-the-changes/), [KPMG 2026 flash alert](https://kpmg.com/xx/en/our-insights/gms-flash-alert/2026/flash-alert-2026-153.html), [GST for freelancers (TaxGuru)](https://taxguru.in/goods-and-service-tax/gst-freelancers-consultants-guide-domestic-foreign-clients.html), [Nishith Desai: PE](https://www.nishithdesai.com/research-and-articles/hotline/tax-hotline/the-home-office-permanent-establishment-in-the-age-of-remote-work-decoding-the-2025-oecd-update-15478), [DPDP roadmap (TCSA)](https://www.tcsa.in/resources/dpdp-rules-2025-implementation-roadmap), [Instahyre salaries](https://resources.instahyre.com/blog/software-engineer-salary-in-india/), [Persol salaries](https://www.persolindia.com/articles/salary-of-senior-software-engineer-in-india)
- **Romania:** [PwC tax summary](https://taxsummaries.pwc.com/romania/individual/other-taxes), [IOI 2025 (unibuc)](https://unibuc.ro/patru-medalii-de-aur-aduse-romanei-de-elevii-olimpici-participanti-la-olimpiada-internationala-de-informatica-2025/?lang=en), [EF EPI](https://www.ef.com/assetscdn/WIBIwq6RdJvcD9bc8RMd/cefcom-epi-site/fact-sheets/2025/ef-epi-fact-sheet-romania-english.pdf), [Folositor 2026 salaries](https://folositor.ro/ghid/cat-castiga-un-programator-in-romania-2026), [Levels.fyi](https://www.levels.fyi/t/software-engineer/locations/romania), [Micro-companies 2026](https://www.fiscalitatea.ro/microintreprindere-in-2026-2-schimbari-importante-pentru-firme-24602/)
