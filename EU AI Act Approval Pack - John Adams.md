# EU AI Act Approval Pack — John Adams

**Lab:** Classify your product · Module 7, Week 7 Day 2 · **Partner:** Gordon S (GordonS)

This single document consolidates the full paired exercise: the hidden client briefs I wrote, my private answer key, the briefs Gordon sent me, my consulting review of Gordon's cases, the full approval pack, and the client debrief — organized by lab phase/CFU checkpoint so each grading criterion is easy to locate.

---

## Phase 1 / CFU 1 — Recognize: hidden client brief (authored by me, for Gordon)

Four client-facing scenarios, category labels stripped, sent to Gordon to review blind. One case per target outcome.

### Case 1 (client-facing)

A group of nightlife venues wants an ID-scanning tool that also lets any venue flag a patron as "problematic" and share that patron's ID scan and photo on a shared network other member venues can view.

### Case 2 (client-facing)

A company's leadership team wants a tool that helps set quarterly goals and KPIs, lets each team build their OKRs against those targets, and tracks progress in one shared planning document.

### Case 3 (client-facing)

A city department wants a tool to scan live crowd video feeds at public demonstrations and match faces in real time against a watchlist, alerting officers on scene to potential matches.

### Case 4 (client-facing)

A company wants a tool that joins sales, customer service, and internal calls, transcribes them automatically, and routes relevant notes (feature requests, promo details, etc.) into the right team's system.

### Private answer key (mine — not shared with Gordon until debrief)

| Case | Intended category | Why |
|---|---|---|
| 1 | High-risk | The system profiles individuals and affects their access to services across multiple venues based on shared flags, not just a one-time document check. |
| 2 | Minimal risk | Internal planning tool with no impact on individuals' rights, no profiling, and no biometric or sensitive personal data involved. |
| 3 | Prohibited | Real-time remote biometric identification of people in public spaces by law enforcement is banned under Article 5, with no applicable narrow exception here. |
| 4 | Limited risk / transparency | The tool doesn't score or profile people, but participants must be told an AI system is recording and transcribing the call. |

One case per required outcome (prohibited, high-risk, limited risk/transparency, minimal risk) — satisfies CFU 1.

---

## Phase 2 / CFU 2 — Apply: Gordon's hidden client briefs (received by me)

Briefs only — Gordon's private answer key was withheld from me until the Phase 4 debrief below.

### Case 1

Outsourced customer service provider, around 400 agents split between Hamburg and Lisbon, running inbound support for three telecom brands. Attrition is high and quality scores swing wildly between team leads, who currently sample two calls per agent per month. They want a system that runs on live call audio and flags agent stress, frustration and "engagement drop" in real time from tone, pitch, speech rate and pause patterns. Output lands on a team lead dashboard and rolls up into a weekly per agent "wellbeing and composure" score that feeds coaching plans and the quarterly performance review. The engine comes from a speech analytics vendor; the client would tune thresholds on its own archived recordings. Team leads can dismiss any flag, and nobody is disciplined automatically.

### Case 2

Private vocational academy in NRW, roughly 1,200 students a year in IT and logistics certifications, partly funded through Bildungsgutschein. They receive about 3,000 applications for 400 subsidised places and the admissions team cannot keep up, while grading of end of module practical write ups varies a lot between instructors. They want one model that ranks applicants using:
- prior grades
- a written motivation text
- a short online aptitude test
- postcode level completion rates from past cohorts

A second model scores practical assessment write ups against a fixed rubric. Admissions staff see the ranked list and can move candidates up or down; instructors see the suggested grade and confirm or change it, and in practice confirm around 90% of the time. Rejected applicants receive a standard letter. Built in house by the academy's two person data team on top of an open weights model.

### Case 3

Real estate marketplace covering DACH, around 90,000 active listings. Agents upload dark, empty, badly framed photos, and listings with weak images get a fraction of the enquiries. Three things are wanted:
- generate photorealistic furnished versions of empty rooms from the agent's own photos
- write the listing description automatically from the structured property data sheet
- run a chatbot on the listing page that answers questions about the property and books viewing slots

Inputs are the uploaded photos, the property data sheet and text from past listings. Agents can edit anything before publishing, though most publish as generated. The people on the other end are buyers and renters browsing listings. The chatbot hands off to a human agent as soon as the conversation turns to price negotiation.

### Case 4

Mid sized beverage producer near Bremen with two bottling lines. Unplanned stoppages cost roughly one shift a week and fill level defects are caught too late, after pallets are already wrapped. They want overhead cameras plus vibration and temperature sensors on the filler and the labeller, with a model that spots bottle defects and predicts bearing failures a few days ahead, feeding a maintenance queue and auto ordering spare parts below a set value. Line operators appear in the camera frame and their badge scans sit in the same timestamped log as the sensor data. Maintenance planners approve every work order before it is issued. Nothing from the system feeds shift planning or individual performance review. Delivered as a managed service by AWS who hosts the models.

### My first-pass classification (Apply — inferred without seeing Gordon's answer key)

| Case | Likely category | Why this is my first-pass call |
|---|---|---|
| 1 | High-risk | The system infers worker stress and feeds a formal performance review. That's employment profiling, an Annex III area, even with team leads able to dismiss flags. |
| 2 | Prohibited | Ranking applicants for subsidized education using postcode completion rates is a proxy for socioeconomic status. It systematically disadvantages poorer areas and denies access to education. That's discriminatory exclusion, not just high-risk scoring. |
| 3 | Limited risk / transparency | The generated "furnished" room photos are synthetic images shown to buyers as if real. Article 50 requires disclosing that an image is AI-generated. The chatbot needs the same disclosure unless it's obvious from context. No decision is made about a person, so this stays below high-risk. |
| 4 | Minimal risk | The system predicts equipment defects and failures, not worker performance, and doesn't feed shift planning or reviews. Workers appearing in camera and badge logs is incidental, not the system's purpose. Under the narrowed safety-component definition, a quality/efficiency tool like this only counts as high-risk if a failure could endanger health or safety, which isn't the case here. |

---

## Phase 2 / CFU 3 — Integrate: proposed architecture, roles, obligations, decision

| Case | Proposed AI architecture | Provider / deployer / vendor | Required obligations or controls | Decision |
|---|---|---|---|---|
| 1 | **Trigger:** live call audio<br>**Model:** infers stress, frustration, and engagement from tone, pitch, rate, and pauses<br>**Human review:** team lead reviews and can dismiss each flag<br>**Output:** weekly per-agent score feeding coaching and performance review<br>**Logging:** archived recordings used to tune thresholds | **Provider:** speech analytics vendor (builds the engine, places it under its own name)<br>**Deployer:** outsourced service provider (Hamburg/Lisbon)<br>**Vendor:** yes, third-party engine | Bias/accuracy testing on training data (Art. 10). Automatic logging, retained 6+ months (Art. 12). Formal human oversight process (Art. 14), not just an informal dismiss button. Agents told they're monitored, with a right to contest a flag. Self-assessment conformity check (Annex VI) — employment is Annex III point 4, not biometrics, so no notified body. FRIA likely not required (private call center, not public service). | **Approve with controls** |
| 2 | **Trigger:** application submitted<br>**Model:** ranks applicants on grades, motivation text, aptitude test, and postcode; second model scores practical write-ups against a rubric<br>**Human review:** admissions can reorder the list; instructors confirm ~90% of suggested grades<br>**Output:** ranked list, standard rejection letters | **Provider:** the academy (built in-house on an open-weights model, placed into service under its own name, Art. 3(3))<br>**Deployer:** same academy<br>**Vendor:** no third party; open-weights base model is a GPAI layer underneath | Deny as proposed. Redesign: drop the postcode variable, score only on individual merit, bias-test the redesigned model (Art. 10), keep human confirmation, document the ranking logic. FRIA likely required — private provider of a publicly subsidized service. | **Deny and redesign** |
| 3 | **Trigger:** agent uploads photos, or a buyer opens the listing/chat<br>**Model:** image generation for staging, text generation for descriptions, chatbot for Q&A and booking<br>**Human review:** agent can edit before publishing, though most publish as-is<br>**Output:** listing images, text, chat replies, booking slot<br>**Disclosure:** label staged images as AI-generated, chatbot identifies itself, hands off to a human at price negotiation | **Provider:** the marketplace platform (builds and ships the finished product under its own name)<br>**Deployer:** individual agents using the platform professionally<br>**Vendor:** likely yes, GPAI model underneath image/text generation | Label AI-generated images (Art. 50). Chatbot discloses itself as AI at the start. Keep existing human handoff for negotiation. Keep a record of what was AI-generated vs. agent-edited. | **Approve with controls** |
| 4 | **Trigger:** sensor and camera feed from the filler and labeller lines<br>**Model:** defect detection and predictive maintenance<br>**Human review:** maintenance planner approves every work order before issuance<br>**Output:** maintenance queue, auto spare-part orders under a set value<br>**Logging:** timestamped sensor, badge, and camera log | **Provider:** the beverage producer (defines and puts the finished system into service under its own name)<br>**Deployer:** the beverage producer, same entity<br>**Vendor:** AWS, hosting and likely supplying the underlying model (GPAI/infrastructure layer) | No AI Act obligations triggered as designed. Separately: tell operators they appear in camera/log data; confirm that data stays out of HR and performance systems. | **Approve** |

---

## Phase 3 — Approval pack (client-facing deliverable)

### Executive summary

Of the four proposed AI systems, one can launch as-is, two can launch with controls, and one cannot launch as designed.

- **Case 1** (call center stress monitoring): high-risk. Approve with controls.
- **Case 2** (admissions ranking): prohibited as designed. Deny and redesign.
- **Case 3** (real estate marketplace tools): limited risk. Approve with controls.
- **Case 4** (bottling line maintenance): minimal risk. Approve.

The one blocker is Case 2. It scores and ranks applicants using postcode as an input, which acts as a proxy for socioeconomic status. Because this scoring gates access to education, and the places involved are government-subsidized, the discrimination risk is more serious than a typical high-risk case. This must be removed before launch.

### Case 1: Call center stress monitoring

**Client:** Outsourced customer service provider, ~400 agents (Hamburg and Lisbon), inbound support for three telecom brands.

**What it does:** Analyzes live call audio and flags agent stress, frustration, and "engagement drop" from tone, pitch, speech rate, and pauses. Produces a weekly per-agent score that feeds coaching and quarterly performance review.

**Category: High-risk.** This is employment profiling, an Annex III area. Team leads can dismiss any flag and no one is auto-disciplined, but human review doesn't change the category. It's a control, not an exemption.

**Architecture and roles:**
- Provider: the speech analytics vendor (builds and names the engine)
- Deployer: the call center
- Human oversight: team lead reviews and can dismiss each flag

**Compliance implications:**
- Bias and accuracy testing on the training data (Article 10)
- Automatic logging, retained 6+ months (Article 12)
- Formal human oversight process (Article 14), not just an informal dismiss button
- Agents must be told they're being monitored
- Agents must have a right to appeal or contest a flag, not just have it silently affect their score
- Self-assessment conformity check (Annex VI); no notified body needed, this isn't biometrics
- Fundamental Rights Impact Assessment (FRIA) likely not required, this is a private call center, not a public service

**Decision: Approve with controls.**

### Case 2: Admissions ranking

**Client:** Private vocational academy in NRW, ~1,200 students/year, subsidized places (Bildungsgutschein).

**What it does:** Ranks ~3,000 applicants for 400 subsidized spots using grades, a motivation text, an aptitude test, and postcode-level completion rates from past cohorts. A second model grades practical write-ups.

**Category: Prohibited, as designed.** Three things stack up here: it's a scoring system, it can discriminate (postcode is a proxy for socioeconomic status), and it gates access to education that is government-subsidized. Systematically disadvantaging poorer applicants for a publicly funded program is discriminatory exclusion.

Open question for the client: does eligibility to apply already depend on postcode (for example, only accepting applicants from certain neighborhoods)? That wasn't stated in the brief, but if true, it would sharpen the discrimination case further and needs to be checked before final sign-off.

**Architecture and roles:**
- Provider: the academy (built in-house, on an open-weights model, placed into service under its own name)
- Deployer: the academy
- Human oversight: admissions can reorder the ranked list; instructors confirm ~90% of suggested grades

**Compliance implications:** None can make the current design compliant. The postcode variable has to go.

**Redesign option (lawful alternative):**
- Drop the postcode variable entirely
- Rank on individual merit only: grades, motivation text, aptitude test, rubric-graded practical
- Add a dedicated scholarship or reserved-spot track for applicants from disadvantaged backgrounds, opted into voluntarily, not scored on postcode by the ranking model
- Bias-test the redesigned model (Article 10)
- Keep human confirmation on both the ranking and the practical grades
- Document the ranking logic and rejection reasoning
- Fundamental Rights Impact Assessment (FRIA) likely required once redesigned: private provider of a publicly subsidized service

**Decision: Deny and redesign.**

### Case 3: Real estate marketplace tools

**Client:** Real estate marketplace, DACH region, ~90,000 active listings.

**What it does:** Generates furnished versions of empty-room photos, writes listing descriptions from property data, and runs a chatbot that answers questions and books viewings.

**Category: Limited risk / transparency.** The generated room photos are synthetic images shown to buyers as if real. Article 50 requires labeling them as AI-generated. The chatbot needs the same disclosure unless it's already obvious. No decision is made about a person, so this stays below high-risk.

**Architecture and roles:**
- Provider: the marketplace platform (builds and ships the finished product under its own name)
- Deployer: individual agents using the platform
- Human oversight: agents can edit before publishing, though most publish as generated

**Compliance implications:**
- Label AI-generated images as AI-generated (Article 50)
- Chatbot must disclose it's AI at the start of a conversation
- Keep the existing human handoff at price negotiation
- Keep a record of what was AI-generated vs. agent-edited

**Decision: Approve with controls.**

### Case 4: Bottling line maintenance

**Client:** Mid-sized beverage producer near Bremen, two bottling lines.

**What it does:** Overhead cameras plus vibration and temperature sensors detect bottle defects and predict bearing failures a few days ahead. Feeds a maintenance queue and auto-orders spare parts below a set value.

**Category: Minimal risk.** This predicts equipment failure, not worker performance, and doesn't feed shift planning or reviews. Under the AI Act's narrowed definition, a quality/efficiency tool like this only counts as high-risk if a failure could endanger health or safety, which isn't the case here.

**Architecture and roles:**
- Provider: the beverage producer (defines and puts the finished system into service under its own name)
- Deployer: the beverage producer, same entity
- Vendor: AWS, hosting and likely supplying the underlying model
- Human oversight: maintenance planner approves every work order before it's issued

**Compliance implications:** None triggered under the AI Act as designed. Separately (not an AI Act requirement, but worth flagging): operators appear in camera and badge logs, so they should be told, and that data should stay out of HR and performance systems going forward.

**Decision: Approve.**

---

## Phase 4 / CFU 5 — Debrief: intended vs. inferred, client discussion, closing note

### Gordon's private answer key (revealed at debrief)

| Case | Intended category | Why (Gordon's reasoning) |
|---|---|---|
| 1 | **Prohibited** | Article 5(1)(f) bans AI systems that infer emotions of a natural person in the workplace, outside narrow medical or safety grounds. Coaching, wellbeing scoring, and performance review are none of those. The human-override control does not save it — Article 5 has no controls escape hatch. |
| 2 | **High-risk** | Annex III point 3: AI used to determine access/admission to education and vocational training, and to evaluate learning outcomes. Both models sit squarely in it. The subtlety is the postcode-level completion feature, which is a proxy-discrimination / Article 10 data-governance problem layered on top of a high-risk (not prohibited) base classification. |
| 3 | **Limited risk / transparency** | Article 50 only — 50(1) for the chatbot, 50(2) machine-readable marking of synthetic images/generated text, 50(4) disclosure where generated imagery depicts a real place. No Annex III area is touched. |
| 4 | **Minimal risk** | Defect detection and predictive maintenance on machinery. No Annex III area, no Article 50 interaction with a person, no Article 5 practice. |

### Intended vs. inferred comparison

| Case | My inferred category | Gordon's intended category | Match? |
|---|---|---|---|
| 1 | High-risk | Prohibited | **Mismatch** — I read the human-override control as keeping it inside Annex III high-risk; Gordon intended Article 5(1)(f) (emotion inference at work) to apply directly, which has no controls exemption. |
| 2 | Prohibited | High-risk | **Mismatch, inverse of Case 1** — I treated the postcode variable as tipping the case into prohibited discriminatory exclusion; Gordon intended a clean Annex III high-risk case with the postcode feature as an Article 10 governance defect to fix with controls, not a reason to deny outright. |
| 3 | Limited risk / transparency | Limited risk / transparency | **Match** |
| 4 | Minimal risk | Minimal risk | **Match** |

Two of four calls matched exactly; the other two landed on opposite ends of the same axis (Case 1 and Case 2 each: one of us called "prohibited," the other "high-risk with controls"), which is exactly the discovery-quality question this lab is designed to surface — the dividing line between a hard Article 5 ban and an Annex III case with a fixable governance defect is not obvious from the brief alone, and reasonable first-pass reviewers can land on either side.

### Regulatory update Gordon flagged (Digital Omnibus, Reg. (EU) 2026/1744, in force 27 July 2026)

- **Case 1:** Article 5 prohibitions have applied since 2 February 2025 — live now, regardless of intended-category debate. Deny.
- **Case 2:** Annex III obligations (if classified high-risk rather than prohibited) now apply from 2 December 2027, not 2 August 2026 — approve with controls, sequenced against that later date.
- **Case 3:** Article 50 was not deferred and applies from 2 August 2026 — the only case with an obligation that bites this month.
- **Case 4:** Unaffected.

### Client discussion (Gordon as client, reacting to my approval pack)

Cases 1, 3, and 4 had no pushback from the client. Case 2 was the only case discussed further.

The client's first position was to launch as designed now, on the reasoning that the Annex III high-risk enforcement deadline is still years out, and by the time the project reaches full production, timelines might work in their favor. Two problems with that argument:

- Case 2 isn't a high-risk timeline question in my read. Prohibited practices under Article 5 have been enforceable since February 2, 2025 — already in force today, not a future deadline to wait out. (Gordon's intended answer treats Case 2 as high-risk rather than prohibited; either way, the postcode variable is not defensible as designed.)
- Building toward a design you already know is unlawful/high-risk-noncompliant just adds redesign cost later, on top of the redesign cost now.

The client also raised budget concerns: redesigning the ranking system is costly given the engineering work already sunk into the postcode-based model.

After discussion, the client agreed to remove postcode as a direct ranking input. They're weighing one open option: keeping postcode only as an eligibility signal to identify applicants from underserved communities for the scholarship track, not as a scoring input in the main ranking model. That's a meaningfully different use, worth a closer look, but it still needs care: eligibility criteria can carry the same proxy-discrimination risk as scoring if it ends up gatekeeping who can apply at all, rather than only expanding who gets extra support. Recommend legal review of the eligibility-only design before it's built.

**Decision stands: Deny and redesign for Case 2 as originally proposed.** The client is proceeding with a redesign; final sign-off on the new design is a separate review.

### Closing note — what changed after the client discussion

The client conversation didn't change my Case 2 decision (deny and redesign), but it changed the framing: initially I treated the postcode variable purely as a bias/discrimination flaw to strip out. After the client raised the sunk-cost argument and proposed the eligibility-only alternative, I now think the more useful next deliverable isn't just "remove postcode" but a scoped legal review of exactly where the line sits between a postcode *eligibility* signal (arguably defensible, expands access) and a postcode *scoring* signal (proxy discrimination, restricts access) — since that distinction is what will actually let the client keep some value from the work already sunk into the model.

---

## Reinforce: borderline arguments, legal-review flags, and next operational artifacts

| Case | Borderline argument / counter-argument | Where legal should verify | Operational artifact needed next |
|---|---|---|---|
| 1 | Could "stress detection" be framed as acoustic health/safety monitoring, exempting it from Article 5(1)(f)? Weak — the exception is read narrowly, and the output feeds performance review, not safety. | Whether Article 5(1)(f)'s medical/safety exception could plausibly cover this use case at all | Employee transparency notice + logging/retention policy (Art. 12) |
| 2 | Could the 90% instructor confirmation rate count as meaningful human oversight (Article 14)? Weak — high near-automatic confirmation is the textbook automation-bias failure, not a safeguard. | Whether an eligibility-only (non-scoring) use of postcode data still carries proxy-discrimination risk | FRIA draft for the redesigned ranking system |
| 3 | Does virtually furnishing a real apartment count as a "deepfake" of an existing scene under Article 50(4)? Arguable — but the stronger exposure is national unfair commercial practices law, not the AI Act. | Whether staged-photo disclosure practices also need review under national consumer-protection rules | AI-generated content disclosure/labeling policy for the platform |
| 4 | Does incidental worker footage + badge data in the same log make performance inference trivially available, even if unused today? Fair as a data-governance point, but it's a GDPR Article 6 / works-council (Betriebsrat, §87 BetrVG) matter, not an AI Act risk-tier question. | Whether the combined camera+badge log needs works-council sign-off independent of AI Act status | Data-segregation policy keeping maintenance logs out of HR systems |

## Stretch: mini implementation roadmap — Case 1 (call center stress monitoring)

Strongest high-risk case (per my classification) to carry into a mini roadmap:

- **What the provider (speech analytics vendor) needs before market placement:** bias/accuracy testing across accents, languages (German/Portuguese), and demographics represented in the Hamburg/Lisbon workforce; technical documentation and risk management file; Annex VI self-assessment conformity check completed and CE-marking-equivalent declaration prepared.
- **What the deployer (call center) needs before first use:** formalized human-oversight procedure replacing the informal "dismiss button" (documented escalation and appeal path for agents); employee notice of monitoring; logging/retention infrastructure (6+ months); confirmation that scores fed into performance review are auditable and contestable.
- **What evidence to request from the vendor:** bias-testing results and methodology, model card or equivalent technical documentation, incident/error-rate history from other deployments, and a data-processing agreement covering the archived-recording tuning data.

---

*This document consolidates and supersedes the standalone files `Client Briefs_JohnA.md`, `Client Briefs_Answer Key_JohnA.md`, `Client Briefs_GordonS.md`, `Client Briefs_Answer Key_GordonS.md`, and `Approval Pack_John Adams.md` for grading purposes; those files remain in the repo as source material.*
