# Lab | Week 7 | Day 2 | Classify your product - Approval Pack
**Prepared by:** John Adams

## Executive summary

Of the four proposed AI systems, one can launch as-is, two can launch with controls, and one cannot launch as designed.

- **Case 1** (call center stress monitoring): high-risk. Approve with controls.
- **Case 2** (admissions ranking): prohibited as designed. Deny and redesign.
- **Case 3** (real estate marketplace tools): limited risk. Approve with controls.
- **Case 4** (bottling line maintenance): minimal risk. Approve.

The one blocker is Case 2. It scores and ranks applicants using postcode as an input, which acts as a proxy for socioeconomic status. Because this scoring gates access to education, and the places involved are government-subsidized, the discrimination risk is more serious than a typical high-risk case. This must be removed before launch.

## Case 1: Call center stress monitoring

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

## Case 2: Admissions ranking

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

## Case 3: Real estate marketplace tools

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

## Case 4: Bottling line maintenance

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

## Closing note

Cases 1, 3, and 4 had no pushback from the client. Case 2 was the only case discussed further.

The client's first position was to launch as designed now, on the reasoning that the Annex III high-risk enforcement deadline is still years out, and by the time the project reaches full production, timelines might work in their favor. Two problems with that argument:

- Case 2 isn't a high-risk timeline question. Prohibited practices under Article 5 have been enforceable since February 2, 2025, already in force today, not a future deadline to wait out.
- Building toward a design you already know is unlawful just adds redesign cost later, on top of the redesign cost now.

The client also raised budget concerns: redesigning the ranking system is costly given the engineering work already sunk into the postcode-based model.

After discussion, the client agreed to remove postcode as a direct ranking input. They're weighing one open option: keeping postcode only as an eligibility signal to identify applicants from underserved communities for the scholarship track, not as a scoring input in the main ranking model. That's a meaningfully different use, worth a closer look, but it still needs care: eligibility criteria can carry the same proxy-discrimination risk as scoring if it ends up gatekeeping who can apply at all, rather than only expanding who gets extra support. Recommend legal review of the eligibility-only design before it's built.

**Decision stands: Deny and redesign for Case 2 as originally proposed.** The client is proceeding with a redesign; final sign-off on the new design is a separate review.
