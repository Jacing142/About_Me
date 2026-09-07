# Jai Goldberg

AI Solutions Engineer. I find the business problems where AI is worth using, then design, build and ship the systems that solve them, end to end.

- Portfolio: https://jais-portfolio-site.vercel.app/
- LinkedIn: https://www.linkedin.com/in/jai-goldberg142
- GitHub: https://github.com/Jacing142

---

## Timeline

| Period | Organisation | Role | Location |
|---|---|---|---|
| 2025–present | Independent | AI Solutions Engineer | London / Remote |
| 2025–present | iPrep | AI Transformation Specialist (part-time) | Remote |
| 2024 | Independent | Partnership Development Consultant | Business Travel |
| 2024–2025 | iPrep | Customer Education Manager | Remote |
| 2023–2024 | iPrep | Instructional Designer, Cognitive Assessment Specialist | Remote |
| 2023 | Oriient | Technical Onboarding Supervisor | Tel Aviv |
| 2022–2023 | Mean It | Cofounder | Remote |
| 2022–2023 | AEI | Research Intern, geopolitics | Herzliya |
| 2021–2022 | Advanced Reality Lab, Reichman University | Research Assistant | Herzliya |
| 2019–2021 | Sachlav | Customer Success / Account Manager | Jerusalem |

## Education and credentials

- Reichman University (IDC) — B.A. Psychology, statistics focus; Minor in Entrepreneurship
- Python: 100 Days of Code (2025)
- Product Analytics, Mixpanel / Product School
- SQL: Data Reporting and Analysis
- International debater (European Championship); debate instructor, 12 students
- TAMID Consulting — built a zero-cost long-term marketing strategy for SodaStream, earning a personal referral from the CEO


---

# Projects

## Bastidian

B2B SaaS for compliance comprehension assessment. Solo build, current.

https://bastidian.vercel.app

**Problem.** Completion logs and multiple-choice pass rates prove that someone clicked, not that they understood. Regulators increasingly require evidence of comprehension, and a completion log is not a defence once an employee actually offends.

**Solution.** A layer sitting on top of an employer's existing training, replacing the post-training multiple-choice test with a conversational assessment. It outputs an executive report plus an audit-ready evidence appendix.

*Conversation design.* A four-stage flow built on Bloom's taxonomy: core question, explanation, application, protégé effect.

*Authoring.* Questions are handwritten by the admin or uploaded from SCORM or Excel, AI-enriched with a human in the loop, then converted into a rubric with a human in the loop. Once approved, the assessment locks and is reusable across unlimited users and runs.

*Scoring.* LLM-as-judge producing binary 1/0 scores against pre-built rubrics rather than holistic scales, so every criterion is measurable. Responses below a confidence threshold route to human review. Three-pass multi-evaluator consensus with a tiebreaker, QA review before delivery, and optional named human review.

*Architecture.* One high-quality Opus call builds the rubrics once, then cheap GPT-4o-mini calls score each response 0/1 against them. Deployed via a Railway worker plus Supabase, using async job processing to work around Vercel timeouts.

*Stack.* Python, LangChain, LangGraph, LLM APIs, Supabase/Postgres, TypeScript with Zod, OAuth.

**My role.** Everything, solo: architecture, build, landing page, sample reports, positioning, outreach.

**Numbers.** Roughly 90% evaluation cost reduction, with output quality improved rather than merely maintained. Approximately $1–2 to build a question, $0.01–0.02 to run it. Five repeat runs against the same tested answers produced consistent results. Sample executive report 24 pages; sample evidence appendix 39 pages.

**Status.** Architecture complete. The landing page is live, with a sample executive report, sample evidence appendix and admin dashboard demo publicly reachable. The MVP is gated behind a contact request because each run carries a cost.

Go-to-market is a target list of 80–100 FCA and FINRA-regulated firms, with discovery calls held with compliance leaders and several client meetings. No revenue, pilots or customers to date.

The beachhead is anti-money-laundering under FCA and FINRA, with a potential move to UK workplace harassment tied to the Employment Rights Act 2025 duty change on 30 October 2026.

**Debugging case: the empty-section pass.** The LLM judge, working from a detailed rubric, was passing responses that missed key details. I found this pre-production using test cases each deliberately wrong in exactly one area.

The root cause was that one criterion's data never reached the database, so the judge read an empty section and skipped it rather than failing it. The fix was twofold: correct the database write, and change the rubric to flag empty sections instead of skipping them.

---

## Validity

End-to-end agentic claim-verification system. Open source.

https://github.com/Jacing142/Validity

Decomposes input into atomic claims, searches for supporting and contradicting evidence, classifies source credibility, and produces a structured verdict.

LangGraph orchestration, WebSocket streaming, human-in-the-loop review modal, MCP server integration. FastAPI backend, React frontend, deployed via Docker.

---

## GenAI Conversation Explorer

Browser-based tool for searching, filtering and merging exported AI conversation logs. Open source.

- Live: https://gen-ai-conversation-searcher-merger.vercel.app
- Source: https://github.com/Jacing142/GenAI-Conversation-Searcher-Merger

Parses, cleans and merges exported data from ChatGPT and Claude, solving broken native search, automated titles and fragmented multi-account exports. Handles file sizes too large for direct re-upload, so users can filter and send curated datasets back into a model for analysis. It removes roughly 70% of irrelevant content.

Pre-LLM PII filtering and local execution mean data never leaves the machine. Built in JavaScript, deployed on Vercel.

100+ signups in the first week, with sustained 100+ weekly active users.

---

## Voice AI virtual agent — POC solution design

An 11-intent NLU voice agent for a fictional restaurant chain contact centre, built in Vonage AI Studio as a Solutions Engineering take-home and delivered in 48 hours.

Includes a three-tier containment framework, a $3.4M year-one ROI model, NLU training data and a full executive deck. Designed for a 150-agent call centre.

The repository is open source and the presentation is my own work; both are publishable.

---

# Work

## Independent practice (2025–present)

Employers are named below. Independent clients are described by industry and scale rather than by name, unless the engagement is already public.

### Order intake pipeline — logistics, Hong Kong

**Problem.** Orders arrived as photographs and emails. Staff manually rewrote the data into a Google Sheet that was then sent to manufacturers. The deals involved are six and seven figures, so transcription errors are expensive.

**Solution.** An intake system that cleans incoming order data, writes it to a Google Sheet ready for QA, then passes it to manufacturing. Built in Google Apps Script with a high confidence threshold set from the start.

**My role.** Discovery, build, ROI projection, rescope.

**The prioritisation miss.** I built the handwritten-photo transcription step first, over two days. At the confidence threshold, not a single handwritten order photo passed without human review, so the projected ROI did not hold against the real inputs.

I took this back to the stakeholders with the reasoning rather than shipping something that saved nothing. I then sat with the employee and watched her do the work rather than asking her about it again, which showed which steps were simple and repetitive from the model's point of view rather than from hers. I rescoped to the SKU-based flow, which cleared the projected ROI.

**Outcome.** What the deployed system passes is correct 99%+ of the time. Two days sunk on the first workflow, caught before it scaled. In production, not running autonomously; the handwritten transcription step is excluded from scope.

### Applicant completion automation — tourism

**Problem.** Applicants stalled mid-funnel. Processing took 5+ weeks per applicant.

**Solution.** A scheduled job finds inactive applicants in Salesforce, which holds the application stage alongside every prior message and human call, so the flow reads contact history rather than running a separate wait loop.

- Pulls personal data from Airtable: phone, email, name, age, who the applicant applied with
- Guards on a "waiting for approval" state, then branches on whether the applicant has connected applications, meaning friends who applied together
- The connected path runs LLM intent detection and template selection
- Selects the preferred channel (Gmail API, Twilio SMS, WhatsApp Business API), sends, checks success, then updates the CRM or queues a retry
- A queuing system caps concurrent LLM calls to prevent runaway usage, with limited retries before human escalation

Built in Python and n8n.

**My role.** Discovery, build, deployment.

**Outcome.** Processing cycle reduced from 5+ weeks to 3 weeks per applicant. Context-aware, relationship-aware personalised nudging running in production with Salesforce logging.

### Operations automation — hospitality

**Problem.** The brief from the Customer Success Manager was "add AI to save money". No scope, no specifics, no success criteria.

**Solution.** I ran separate discovery sessions with the manager and with frontline employees, because they had different problems. The manager wanted efficiency, employees wanted less friction, and the C-suite wanted a number.

I mapped actual pain points with quantifiable time costs. Without perfect data, I prioritised a time-saving framing over cost-cutting, as more tangible and easier to adopt. I proposed three automations, each with a quantified metric, and secured sign-off on the metrics before building anything.

The build was AI intake → intent classification → validation → routing, in n8n with LLMs, including logging, retry handling and failure monitoring.

**My role.** Multi-level discovery, scoping, metric agreement, build, delivery.

**Outcome.** Minimum 25 minutes saved per employee per day across a 20-person team, rising to 3 hours in peak season. Three automations delivered: personalised nudging, email triage, support chatbot.

### AI agent review and guardrail rebuild — D2C ecommerce, India

A 150–200 person company transitioning to AI-first, handling tens of thousands of AI interactions daily across 8+ languages.

**Problem.** Internal and customer-facing agents were running at scale with no guardrails, no analytics, and in some cases no system prompt at all. Prompts ran to 300–400 lines. Customer data was reaching the model unmasked. There was no ML expertise in-house.

Agents in scope included an internal analyst agent that staff queried about customer segments and product ideas, and a customer-facing AI tarot reader.

**Solution.** A written document of recommended improvements, plus hands-on fixes made alongside their team.

The largest changes were to system prompts and model parameters, brand voice, and the introduction of reusable assets defined at company level — brand voice, tone, guardrails, system prompts and skills — shared across every agent rather than each team rebuilding its own.

**Outcome.** Roughly 20% of conversations were starting in the correct language then switching mid-conversation. This was brought below 1%. Recommendations actioned.

### Ad and commerce data unification — D2C ecommerce, India

**Problem.** Data was spread across Shopify, Google Ads, Meta Ads, Google Analytics, ClickPost, ShipRocket, QuickEngage and a separate SQL database. Reporting ran on Pabbly plus manual CSV export into Google Sheets, cleaned in-sheet, with reports written by hand.

The stated number one friction was merging Meta Ads and Google Ads data. The goal was a single source, queryable in natural language by the whole company rather than only by analysts.

**Solution.** Discovery first, establishing the operating parameters: roughly ₹800 average order value, around 200 SKUs, 40–60 orders per day, 1,200–1,600 orders per month, with history from September 2025.

I delivered an 18-slide deck for a mixed technical and non-technical decision-making audience, structured as current state and ROI, then a brief data-flow overview, then stage-by-stage technical detail.

*Architecture.* Fivetran ingestion, BigQuery in the Indian region, Fivetran Quickstart and dbt models for transformation, Google Sheets for consumption with a chatbot layer later.

*Staging.* Stage 1 the Google and Meta ad merge, achievable in days on free tiers. Stage 2 an owned dbt project, one to two weeks. Stage 3 ClickPost, the SQL database and the chatbot. I recommended the client approve Stage 1 only.

**My role.** Discovery, architecture selection, deck, presentation. I built the first stage myself.

**Outcome.** Deck delivered, presented and accepted. The client is building the remainder in-house from the recommendation; the engagement is closed.

### Personalised psychometric feedback engine — education, US

**Problem.** Producing personalised narrative feedback per candidate, per trait, per target role was manual and did not scale.

**Solution.** An LLM pipeline in Google Apps Script calling the Claude API.

- Reads persona, trait definition, question bank and score sheets into lookup maps, then loops trait by role, batching every question for a trait-and-role pair into a single call
- A long system prompt carries 12 numbered writing rules and an editorial self-review standard
- An explicit flip map inverts target answers for reverse-scored items, with midpoint targets deliberately mapping to themselves. Reverse items receive a fixed opening line injected verbatim rather than generated
- Responses parsed by regex per profession block, with missing blocks written as a parsing error rather than shifting rows
- Checkpoint and resume via PropertiesService against a five-minute budget, under Apps Script's six-minute ceiling
- Per-pair try/catch so one failure does not abort the run, with a custom Sheets menu for start, resume, reset and checkpoint check
- A separate rubric-based QA pass runs after generation

**My role.** Designed and built the entire pipeline solo, including scoring logic, validation layers and the rubric review pass.

**Outcome.** 18,600 reports generated across three Hogan instruments, with 85% less production time per entry, zero escalations to human review, no edits found in QA sampling, and $15 total API cost.

### AI opportunity assessment — international school, New Delhi

Family-owned international school. Prospective client; no contract signed.

**Problem.** The school had spent one to two years building roughly 28 interconnected internal products, developed from teacher interviews, with an in-house PHP engineer and almost no AI in the stack. They had no view of where AI would actually pay back across that estate.

**Solution.** I reviewed their existing product design and roadmap and consulted on direction.

I scoped and designed a per-student persona and opportunity-matching system: it builds a persona from accomplishments, interests, goals and grades, then recommends opportunities such as competitions, speeches and groups, aimed particularly at less confident students. A proof of concept was built.

I then built and presented a board-level deck laying out AI opportunities and ROI in time and cost across their existing products, written in board language, with evaluation, guardrails and running cost included.

**My role.** Discovery, product design consultation, system design, proof of concept, deck, presentation.

**Outcome.** The school intends to continue the work internally. No contract.

### AI fluency workshops — GTM teams

Customer Success and Sales teams were not integrating AI tools into daily work. I delivered approximately 10 live workshops, training 100+ staff, with roughly 90% daily adoption reported by managers. The adoption figure is manager attestation rather than measured data.

---

## iPrep (2023–present)

Test-prep e-learning provider serving 20,000+ learners across Israel and the US.

I joined as an instructional designer, was promoted within a year to Customer Education Manager, and then moved into AI implementation, becoming the CEO's primary contact for AI and automation work. I am now part-time on retainer.

### Learner support virtual agent

**Problem.** The company was handling 300+ recurring support tickets a month. Passive FAQ pages were not converting, so users hit a wall and emailed support.

The blocker was not technical. The C-suite did not trust AI on consistency, and had no appetite for a customer-facing bot getting things wrong in public.

**Solution.** A production LLM chatbot with an intent taxonomy, dialogue scripts, and RAG over the LMS knowledge base.

- 75% confidence threshold, below which the bot hands off to a human with full captured context
- Fallback and clarification prompts with loop limits
- Analytics from launch, with weekly review of real failure paths

The escalation path is the hallucination control. The bot does not guess.

**My role.** I read the C-suite concern as a trust risk rather than a cost risk, and set CSAT as the primary metric with deflection secondary, stated upfront.

I pulled ticket and FAQ data to identify the highest-volume issue and scoped the MVP narrowly around that one path. I built the happy path first, then edge cases, then escalation logic. I presented MVP results to convert the pilot into a full build, and scaled only once the analytics held. I made the build-versus-buy call in favour of building.

Solo build: two weeks to MVP sign-off, two weeks to build the initial intents, four weeks of analytics before scaling.

**Outcome.** Support tickets reduced from 300 to 210 per month, a 30% reduction, with CSAT held at 4.8/5 across 20,000+ learners. The first AI product in production at the company. Maintained, monitored and iterated for several months post-launch.

### Completion rate rebuild

**Problem.** Course completion was stuck low across several programmes. The internal assumption was that the content needed updating.

**Solution.** Behavioural analysis over xAPI and GA4, mapping drop-off by course, section and content type, cross-referenced against support tickets.

I segmented the drop-offs by where they occurred: early drop-off as a framing problem, mid-course as pacing and friction, near-completion as motivation and perceived value. I then rebuilt the journey architecture around that segmentation.

**My role.** Pulled and analysed the data, challenged the internal hypothesis, built a prioritised recommendation with projected improvements, presented findings and specific changes to stakeholders, and implemented.

**Outcome.** Completion improved from 16% to 42% across the lowest-performing programmes. Post-assessment scores improved from 68% to 84% through scenario-based redesign and cohort analysis. Journey architecture, not content quality, was the driver.

### Content and course production automation

**Problem.** Content creation ran at roughly 20 hours per module. Nobody had asked for change, and automation was not on the roadmap.

**Solution.** I mapped the production process in detail, identified the manual and automatable steps, and built and shipped the automations.

This extended into an agentic workflow that turns SME input and existing course material into outlines, then, after human review, into video scripts, visual suggestions and assessment questions. Human review gates are retained at each stage.

Built with Google Apps Script, LLM APIs and n8n.

**My role.** I built the business case unprompted: time saved per cycle, projected output increase, cost against saving. I pre-empted quality and adoption objections inside the proposal, pitched the CEO directly as a growth lever rather than a process complaint, secured internal budget, and built it.

**Outcome.** Production cycles reduced from 20 hours to 12 hours per module. Self-initiated with no mandate. Freed enough capacity to take on outside projects with CEO approval.

### Cognitive skills learning platform

Built a test preparation programme for cognitive assessments used in hiring, reaching 10,832 learners with 565 verified reviews at 4.7 stars. Combined practice exercises, video instruction and progressive skill building to improve performance on high-stakes HR screening tests.

### Scanner rollout training

A complex technical system required rollout training at scale. I translated the operational workflows into adoption-ready learning paths and designed the full programme, working effectively solo with SME input. Delivered to 10,000+ users.

### Instructional video production

Produced thousands of training videos end to end: scripting, recording, editing and publishing. Built in Canva and Clipchamp, published to YouTube. Narration was later migrated to ElevenLabs AI voice.

---

## Oriient — Technical Onboarding Supervisor (2023)

Indoor positioning SaaS, with enterprise retail deployments across Australia, Canada, the UK and the US.

**Problem.** In-store mapping was carried out by distributed freelance contractors. Rework was high and contractor ramp-up was slow across multiple markets. Time zone and cultural variation was a real operational variable, not a soft one.

**Solution.** Remote onboarding and QA of contractors, with defined handoff structures and escalation paths into engineering and the client-facing team.

Onboarding explanations were adapted culturally while QA standards stayed constant. I co-redesigned the onboarding and QA playbooks with engineering, and built a shared living document of cultural references, analogies and communication patterns that teammates contributed to and engineers used when writing product updates.

**My role.** Onboarding, QA, escalation, playbook redesign, and supervision of 6 to 8 mappers.

**Outcome.** 150+ enterprise deployments including Walmart and Albertsons stores, with first-time mapping accuracy improved from 70% to 95%. Retained through a company-wide restructuring despite being the most recent hire on the team, and offered rehire when funding recovered.

*Scope note:* the Walmart and Albertsons work was conducted with individual stores' freelance mapping staff, not with Walmart's enterprise organisation.

---

## Mean It — Cofounder (2022–2023)

Two-sided consumer analytics platform.

**Problem.** Quantitative data tells companies what happened, never why. Consumers, meanwhile, had no reason to hand over the qualitative layer that would explain it.

**Solution.** Individuals receive personalised insights they can act on; companies receive aggregated consumer and segmentation data. I ran consumer discovery to validate the pain and find fit, determined which data points mattered most, and built onboarding to capture them.

**My role.** Directed a team of six: two technical, one business, one psychology and behaviour, one design, plus myself. Peer and cofounder leadership rather than line management.

- Set goals, ran meetings, owned structure, divided ownership, presented, and entered the team into demo days and pitch nights
- Built pitch decks, landing page and demo
- Owned and prioritised the backlog against activation data
- Built sales enablement assets: objection-handling cards, discovery question sets, value-proposition guides
- Ran research on zero marketing budget through direct interviews, peer networks and early-access signups

**Outcome.** Activation improved from 20% to 80%. Hundreds of beta testers voluntarily submitting personal data. Finals at two pitch nights, hosted at Apple and Microsoft. Met with VCs.

**Why it wound down.** Despite genuine consumer demand, the company wound down on technical scaling. Data collection was manual and individual, with no API available; tech companies were legally obliged under GDPR to hand over user data on request, and preferred to take the fine. Activation also required a personal conversation per user, so growth was bounded by my own time. Neither constraint was visible until we tried to grow.

---

## Sachlav — Customer Success / Account Manager (2019–2021)

Tourism company, Jerusalem. The role was sales.

**Problem.** B2C sales volume and B2B university partnerships both ran on a recurring seasonal cycle, twice a year across two terms, so the funnel reset every season. Implementation time was slowing partner delivery.

**Solution.** Sold direct to consumers at volume and managed the B2B university relationships behind them, running implementation plans, proactive relationship management and expectation alignment. I rolled out a training programme to compress implementation time.

**Outcome.**

- Approximately 600 B2C sales and 20 B2B university partnerships managed
- 95% renewal rate, 75% referral rate
- $300K+ in customer deployments per season; top performer on a 12-person team
- Implementation time reduced from 5 weeks to 2 weeks after the training rollout, raising the team referral rate by 40%

---

## Partnership Development Consultant (2024, four months)

**Problem.** A private investor with holdings across many companies wanted to identify where philanthropic giving to educational institutions and NGOs would also further his business interests. The institutions wanted access to the funding and needed a route to it.

**Solution.** I visited educational institutions and NGOs and ran discovery conversations to understand what each needed, then produced needs assessments and written partnership-opportunity documents and passed them to the decision maker.

**Outcome.** 1,200+ strategic outreaches, 300+ discovery meetings, 40+ strategic partnerships, and a $3M+ pipeline.

---

## Research roles

**AEI — Research Intern, geopolitics (2022–2023).** Research focused on educational terrorism, tracing grant money through funding chains. Presented findings to senior researchers and an ambassador.

**Advanced Reality Lab, Reichman University — Research Assistant (2021–2022).** Set up VR hardware and Unity environments for behavioural anxiety research. Onboarded participants and kept technical systems running through experimental protocols.

---

# Documented outcomes

| Outcome | Value | Context |
|---|---|---|
| Support ticket deflection | 300 → 210 per month (30%) | iPrep, production LLM chatbot |
| CSAT | 4.8/5 across 20,000+ learners | iPrep, held through chatbot rollout |
| Course completion | 16% → 42% | iPrep, lowest-performing programmes, xAPI/GA4 |
| Post-assessment scores | 68% → 84% | iPrep, scenario-based redesign |
| Content production cycles | 20h → 12h per module | iPrep, agentic workflow with human review gates |
| Programme scope | 30 parallel programmes, ~$500K ARR contribution | iPrep, employment scope |
| Cognitive skills platform | 10,832 learners, 565 reviews at 4.7 stars | iPrep |
| Scanner rollout training | 10,000+ users | iPrep |
| Training videos | Thousands, produced end to end | iPrep |
| Enterprise deployments | 150+, including Walmart and Albertsons, across AU/CA/UK/US | Oriient |
| First-time mapping accuracy | 70% → 95% | Oriient |
| Team supervised | 6–8 mappers | Oriient |
| Activation rate | 20% → 80% | Mean It |
| Early traction | Hundreds of beta testers; finals at two pitch nights (Apple, Microsoft); VC meetings | Mean It |
| Sales volume | ~600 B2C sales, 20 B2B university partnerships | Sachlav, recurring twice yearly across two terms |
| Renewal and referral | 95% renewal, 75% referral, team referral +40% | Sachlav |
| Deployment value | $300K+ per season; top performer on a 12-person team | Sachlav |
| Implementation time | 5 weeks → 2 weeks | Sachlav, after training programme rollout |
| Partnership development | 1,200+ outreaches, 300+ meetings, 40+ partnerships, $3M+ pipeline | Four-month engagement |
| Feedback engine output | 18,600 reports, 85% less production time per entry, zero escalations, $15 total API cost | Three Hogan instruments, education client |
| Applicant processing cycle | 5+ weeks → 3 weeks per applicant | Tourism client, personalised nudging |
| Operations time saved | 25+ min per employee per day across a 20-person team, up to 3h in peak | Hospitality client, three automations |
| Order intake accuracy | 99%+ of what the system passes | Logistics client, high confidence threshold |
| Agent language drift | ~20% → under 1% | D2C ecommerce client, 8+ languages |
| AI workshops | ~10 delivered, 100+ trained, ~90% adoption | Adoption is manager attestation, not measured |
| Evaluation cost | ~90% reduction; ~$1–2 per question built, ~$0.01–0.02 per run | Bastidian, quality improved |
| Bastidian pipeline | 80–100 firm target list, discovery calls held | No revenue, pilots or customers to date |
| Conversation Explorer usage | 100+ weekly active users; 100+ signups in week one | |
| Voice agent POC | 11 intents, three-tier containment, $3.4M ROI model | Take-home assignment, 48 hours |

---

# Technical capabilities

**Languages.** Python · JavaScript · TypeScript · SQL · HTML/CSS

**LLM and AI frameworks.** LLM APIs (Claude, GPT, Gemini) · LangChain · LangGraph · FastAPI · Ragas · search APIs (Serper, You.com) · ElevenLabs · Synthesia/HeyGen · NotebookLM

**Automation and integration.** n8n · Zapier · Google Apps Script · REST APIs and webhooks · Vonage AI Studio · Base44

**Data and storage.** Postgres/Supabase · vector and relational databases · Airtable · BigQuery

**Deployment and infrastructure.** Vercel · GitHub · Claude Code and Claude Design · AWS · Azure

**Analytics.** Mixpanel · GA4 · xAPI

**CRM and support.** Salesforce · Intercom · Zendesk · Monday

**Learning and content.** LearnDash · Articulate 360 · Moodle · Canva

Beyond the custom builds documented above, I have built support virtual agents for several clients on Intercom.
