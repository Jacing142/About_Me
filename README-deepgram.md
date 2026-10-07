<!--
DRAFT, written by Claude Code on 7 Oct 2026 for Jai to rewrite.
Condensed from README.md (commit 1761a82) so the Deepgram tier of Virtual J_AI fits its 25,000-character prompt cap.
Rule used: AI and automation work kept at full detail; pre-2023 career cut to headlines plus every number; no facts, figures or statuses changed.
This comment is stripped before the text reaches the agent.
-->

# Jai Goldberg

AI Solutions Engineer | AI Transformation.
I find the business problems where AI is worth using, then design, build and ship the systems that solve them, end to end.

## Timeline

- 2025–present: Independent, AI Solutions Engineer, London / Remote
- 2025–present: iPrep, AI Transformation Specialist (part-time), Remote
- 2024: Independent, Partnership Development Consultant, Business Travel
- 2024–2025: iPrep, Customer Education Manager, Remote
- 2023–2024: iPrep, Instructional Designer, Cognitive Assessment Specialist, Remote
- 2023: Oriient, Technical Onboarding Supervisor, Tel Aviv
- 2022–2023: Mean It, Cofounder, Remote
- 2022–2023: AEI, Research Intern, geopolitics, Herzliya
- 2021–2022: Advanced Reality Lab, Reichman University, Research Assistant, VR, Herzliya
- 2019–2021: Sachlav, Customer Success / Account Manager, Jerusalem

## Education and credentials

Reichman University (IDC), B.A. Psychology with a statistics focus and a minor in Entrepreneurship. Python: 100 Days of Code (2025), plus courses in product analytics and SQL. International debater at the European Championship.

# Work

## Independent practice (2025–present)

Employers are named below. Independent clients are described by industry.

### Order intake pipeline — logistics, Hong Kong

**Problem.** Orders arrived as photographs and emails. Staff manually rewrote the data into a Google Sheet that was then sent to manufacturers. The deals involved are six and seven figures, so transcription errors are expensive.

**Solution.** An intake system that cleans incoming order data, writes it to a Google Sheet ready for QA, then passes it to manufacturing. Built in Google Apps Script with a high confidence threshold set from the start.

**My role.** Discovery, build, ROI projection, rescope.

**The prioritisation miss.** I built the handwritten-photo transcription step first, over two days. At the confidence threshold, not a single handwritten order photo passed without human review, so the projected ROI did not hold against the real inputs. I took that back to the stakeholders with the reasoning rather than shipping something that saved nothing. I then sat and watched the employee do the work rather than asking her again, which showed which steps were simple and repetitive from the model's point of view rather than from hers. I rescoped to the SKU-based flow, which cleared the projected ROI.

**Outcome.** What the deployed system passes is correct 99%+ of the time. Two days sunk on the first workflow, caught before it scaled. In production, not running autonomously; the handwritten transcription step is excluded from scope.

### Applicant completion automation — tourism

**Problem.** Applicants stalled mid-funnel. Processing took 5+ weeks per applicant.

**Solution.** A scheduled job finds inactive applicants in Salesforce, which holds the application stage alongside every prior message and human call, so the flow reads contact history rather than running a separate wait loop. It pulls personal data from Airtable, guards on a "waiting for approval" state, then branches on whether the applicant has connected applications, meaning friends who applied together. The connected path runs LLM intent detection and template selection, picks the channel, sends, and updates the CRM or queues a retry. A queuing system caps concurrent LLM calls, with limited retries before escalation. Built in Python and n8n.

**My role.** Discovery, build, deployment.

**Outcome.** Processing cycle reduced from 5+ weeks to 3 weeks per applicant. Running in production with Salesforce logging.

### Operations automation — hospitality

**Problem.** The brief from the Customer Success Manager was "add AI to save money". No scope, no specifics, no success criteria.

**Solution.** I ran separate discovery sessions with the manager and with frontline employees, because they had different problems: the manager wanted efficiency, employees wanted less friction, and the C-suite wanted a number. I mapped pain points with quantifiable time costs, prioritised a time-saving framing over cost-cutting as more tangible and easier to adopt, proposed three automations each with a quantified metric, and got sign-off on the metrics before building. The build was AI intake, intent classification, validation and routing, in n8n with LLMs, with logging, retry handling and failure monitoring.

**My role.** Multi-level discovery, scoping, metric agreement, build, delivery.

**Outcome.** Minimum 25 minutes saved per employee per day across a 20-person team, rising to 3 hours in peak season. Three automations delivered: personalised nudging, email triage, support chatbot.

### AI agent review and guardrail rebuild — D2C ecommerce, India

A 150–200 person company transitioning to AI-first, handling tens of thousands of AI interactions daily across 8+ languages.

**Problem.** Internal and customer-facing agents were running at scale with no guardrails, no analytics, and in some cases no system prompt at all. Prompts ran to 300–400 lines. Customer data was reaching the model unmasked. There was no ML expertise in-house. Agents in scope included an internal analyst agent that staff queried about customer segments and product ideas, and customer-facing agents.

**Solution.** A written document of recommended improvements, plus hands-on fixes made alongside their team. The largest changes were to system prompts and model parameters, brand voice, and the introduction of reusable assets defined at company level, meaning brand voice, tone, guardrails, system prompts and skills shared across every agent rather than each team rebuilding its own.

**Outcome.** Roughly 20% of conversations were starting in the correct language then switching mid-conversation. This was brought below 1%. Recommendations actioned.

### Ad and commerce data unification — D2C ecommerce, India

**Problem.** Data was spread across Shopify, Google Ads, Meta Ads, Google Analytics, ClickPost, ShipRocket, QuickEngage and a separate SQL database. Reporting ran on Pabbly plus manual CSV export into Google Sheets, cleaned in-sheet, with reports written by hand. The stated number one friction was merging Meta Ads and Google Ads data. The goal was a single source, queryable in natural language by the whole company rather than only by analysts.

**Solution.** Discovery first, establishing the operating parameters: roughly ₹800 average order value, around 200 SKUs, 40–60 orders per day, 1,200–1,600 orders per month, with history from September 2025. I delivered an 18-slide deck for a mixed technical and non-technical audience. The architecture was Fivetran ingestion, BigQuery in the Indian region, dbt models for transformation, and Google Sheets for consumption. I staged it in three: the Google and Meta ad merge first, achievable in days on free tiers, then an owned dbt project, then ClickPost, the SQL database and a chatbot layer. I recommended the client approve Stage 1 only.

**My role.** Discovery, architecture selection, deck, presentation. I built the first stage myself.

**Outcome.** Deck delivered, presented and accepted. The client is building the remainder in-house from the recommendation; the engagement is closed.

### Personalised psychometric feedback engine — education, US

**Problem.** Producing personalised narrative feedback per candidate, per trait, per target role was manual and did not scale.

**Solution.** An LLM pipeline in Google Apps Script calling the Claude API. It batches every question for a trait-and-role pair into a single call, under a system prompt carrying 12 numbered writing rules and an editorial self-review standard. An explicit flip map inverts target answers for reverse-scored items. Responses are parsed by regex per profession block, with missing blocks written as a parsing error rather than shifting rows. Checkpoint and resume run under Apps Script's six-minute ceiling, with per-pair error handling so one failure does not abort the run.

**My role.** Designed and built the entire pipeline solo, including scoring logic, validation layers and the QA sampling.

**Outcome.** 18,600 reports generated across three Hogan instruments, with 85% less production time per entry and $15 total API cost. 5% of generated reports were manually QAed after generation. Zero edits were needed.

### AI opportunity assessment — international school, New Delhi

Family-owned international school. Prospective client; no contract signed.

**Problem.** The school had spent one to two years building roughly 28 interconnected internal products, developed from teacher interviews, with an in-house PHP engineer and almost no AI in the stack. They had no view of where AI would actually pay back across that estate.

**Solution.** I reviewed their product design and roadmap and consulted on direction. I scoped and designed a per-student persona and opportunity-matching system: it builds a persona from accomplishments, interests, goals and grades, then recommends opportunities such as competitions, speeches and groups, aimed particularly at less confident students. A proof of concept was built. I then built and presented a board-level deck laying out AI opportunities and ROI in time and cost across their products, with evaluation, guardrails and running cost included.

**Outcome.** The school intends to continue the work internally. No contract.

### AI fluency workshops — GTM teams

Customer Success and Sales teams were not integrating AI tools into daily work. I delivered approximately 10 live workshops, training 100+ staff, with roughly 90% daily adoption reported by managers. The adoption figure is manager attestation rather than measured data.

## iPrep (2023–present)

Test-prep e-learning provider serving 20,000+ learners across Israel and the US. I joined as an instructional designer, was promoted within a year to Customer Education Manager, and then moved into AI implementation, becoming the CEO's primary contact for AI and automation work. I am now part-time on retainer. My employment scope covered 30 parallel programmes, contributing roughly $500K ARR.

### Learner support virtual agent

**Problem.** The company was handling 300+ recurring support tickets a month. Passive FAQ pages were not converting, so users hit a wall and emailed support. The blocker was not technical: the C-suite did not trust AI on consistency, and had no appetite for a customer-facing bot getting things wrong in public.

**Solution.** A production LLM chatbot with an intent taxonomy, dialogue scripts, and RAG over the LMS knowledge base. A 75% confidence threshold, below which the bot hands off to a human with full captured context. Fallback and clarification prompts with loop limits. Analytics from launch, with weekly review of real failure paths. The escalation path is the hallucination control. The bot does not guess.

**My role.** I read the C-suite concern as a trust risk rather than a cost risk, and set CSAT as the primary metric with deflection secondary, stated upfront. I pulled ticket and FAQ data to find the highest-volume issue and scoped the MVP narrowly around that one path, building the happy path first, then edge cases, then escalation logic. I converted the pilot into a full build on the MVP results, scaled only once the analytics held, and made the build-versus-buy call in favour of building. Solo build: two weeks to MVP sign-off, two weeks for the initial intents, four weeks of analytics before scaling.

**Outcome.** Support tickets reduced from 300 to 210 per month, a 30% reduction, with CSAT held at 4.8/5 across 20,000+ learners. The first AI product in production at the company. Maintained, monitored and iterated for several months post-launch.

### Completion rate rebuild

**Problem.** Course completion was stuck low across several programmes. The internal assumption was that the content needed updating.

**Solution.** Behavioural analysis over xAPI and GA4, mapping drop-off by course, section and content type, cross-referenced against support tickets. I segmented the drop-offs by where they occurred: early drop-off as a framing problem, mid-course as pacing and friction, near-completion as motivation and perceived value. I then rebuilt the journey architecture around that segmentation.

**My role.** Pulled and analysed the data, challenged the internal hypothesis, built a prioritised recommendation, presented to stakeholders, and implemented.

**Outcome.** Completion improved from 16% to 42% across the lowest-performing programmes. Post-assessment scores improved from 68% to 84% through scenario-based redesign and cohort analysis. Journey architecture, not content quality, was the driver.

### Content and course production automation

**Problem.** Content creation ran at roughly 20 hours per module. Nobody had asked for change, and automation was not on the roadmap.

**Solution.** I mapped the production process, identified the manual and automatable steps, and built and shipped the automations. This extended into an agentic workflow that turns SME input and existing course material into outlines, then, after human review, into video scripts, visual suggestions and assessment questions. Human review gates are kept at each stage. Built with Google Apps Script, LLM APIs and n8n.

**My role.** I built the business case unprompted: time saved per cycle, projected output increase, cost against saving. I pre-empted quality and adoption objections inside the proposal, pitched the CEO directly as a growth lever rather than a process complaint, secured internal budget, and built it.

**Outcome.** Production cycles reduced from 20 hours to 12 hours per module. Self-initiated with no mandate. Freed enough capacity to take on outside projects with CEO approval.

### Other iPrep work

A cognitive skills learning platform for assessments used in hiring, reaching 10,832 learners with 565 verified reviews at 4.7 stars. Scanner rollout training: I turned operational workflows into adoption-ready learning paths and designed the programme solo with SME input, delivered to 10,000+ users.

## Earlier career (2019-2023)

**Oriient, Technical Onboarding Supervisor (2023).** Indoor positioning SaaS with enterprise retail deployments across Australia, Canada, the UK and the US. Mapping was done by distributed freelance contractors, with high rework and slow ramp-up. I onboarded and QAed them remotely, co-redesigned the onboarding and QA playbooks with engineering, and supervised 6 to 8 mappers. Outcome: 150+ enterprise deployments including Walmart and Albertsons stores, and first-time mapping accuracy from 70% to 95%.

*Scope note:* the Walmart and Albertsons work was with individual stores' freelance mapping staff, not with Walmart's enterprise organisation.

**Mean It, Cofounder (2022-2023).** Two-sided consumer analytics: personalised insights for individuals, aggregated segmentation data for companies. I directed a team of six. Outcome: activation from 20% to 80%, hundreds of beta testers, finals at two pitch nights hosted at Apple and Microsoft, and VC meetings. It wound down on technical scaling.

**Partnership Development Consultant (2024, four months).** A private investor wanted to find where giving to educational institutions and NGOs would also further his business interests. Outcome: 1,200+ outreaches, 300+ meetings, 40+ partnerships, and a $3M+ pipeline.

**Sachlav, Customer Success / Account Manager (2019-2021).** Tourism company in Jerusalem; the role was sales, on a seasonal cycle that reset twice a year. Outcome: about 600 B2C sales, 20 B2B partnerships, 95% renewal, 75% referral, and implementation time from 5 weeks to 2 weeks, raising the team referral rate by 40%.

# Projects

## Bastidian

B2B SaaS for compliance comprehension assessment. Solo build, current. There is an open demo on the Bastidian site.

**Problem.** Completion logs and multiple-choice pass rates prove that someone clicked, not that they understood. Regulators increasingly require evidence of comprehension, and a completion log is not a defence once an employee actually offends.

**Solution.** A layer sitting on top of an employer's existing training, replacing the post-training multiple-choice test with a conversational assessment. It outputs an executive report plus an audit-ready evidence appendix. The conversation is a four-stage flow built on Bloom's taxonomy: core question, explanation, application, protégé effect. Questions are handwritten by the admin or uploaded from SCORM or Excel, AI-enriched and turned into a rubric with a human in the loop at both steps, then locked and reusable. Scoring is LLM-as-judge producing binary one or zero scores against those rubrics rather than holistic scales, so every criterion is measurable, with low-confidence responses routed to human review, three-pass consensus with a tiebreaker, and QA review before delivery. One high-quality Opus call builds the rubrics once, then cheap GPT-4o-mini calls score each response against them. Built in Python with LangChain and LangGraph on Supabase and Postgres, with a Railway worker and async job processing.

**My role.** Everything, solo: architecture, build, landing page, sample reports, positioning, outreach.

**Numbers.** Roughly 90% evaluation cost reduction, with output quality improved rather than merely maintained. Approximately $1–2 to build a question, $0.01–0.02 to run it. Five repeat runs against the same answers produced consistent results.

**Status.** Architecture complete. A working demo is open to anyone, with no contact request needed. No revenue, pilots or customers to date.

## Validity

End-to-end agentic claim-verification system, open source on my GitHub. It decomposes input into atomic claims, searches for supporting and contradicting evidence, classifies source credibility, and produces a structured verdict. LangGraph orchestration, WebSocket streaming, a human-in-the-loop review modal and MCP server integration, with a FastAPI backend and React frontend.

## GenAI Conversation Explorer

A browser-based tool for searching, filtering and merging exported AI conversation logs, open source and live on Vercel. It parses, cleans and merges exports from ChatGPT and Claude, solving broken native search, automated titles and fragmented multi-account exports, and handles files too large to re-upload. Exports are processed locally in the browser. Built in JavaScript. Sustained 100+ weekly active users, measured in Mixpanel.

## Voice AI virtual agent, proof-of-concept solution design

An 11-intent NLU voice agent for a fictional restaurant chain contact centre, designed for Vonage AI Studio and a 150-agent call centre. It includes a three-tier containment framework, a $3.4M year-one ROI model, NLU training data and a full executive deck. This was a 48-hour Solutions Engineering take-home for Vonage, the brand is fictional, and it reached the final round.

# Technical capabilities

**Languages.** Python, JavaScript, SQL, HTML and CSS.

**LLM and AI.** LLM APIs for Claude, GPT and Gemini, LangChain, LangGraph, FastAPI, Ragas, search APIs, ElevenLabs, Synthesia, HeyGen, NotebookLM.

**Automation, data and infrastructure.** n8n, Zapier, Google Apps Script, REST APIs and webhooks, Vonage AI Studio, Base44, Postgres and Supabase, vector and relational databases, Airtable, BigQuery, Vercel, GitHub, Claude Code, AWS, Azure.

**Analytics, CRM and content.** Mixpanel, GA4, xAPI, Salesforce, Intercom, Zendesk, Monday, LearnDash, Articulate 360, Moodle, Canva.

Beyond the custom builds above, I have built support virtual agents for several clients on Intercom.
