# The AI Diplomat — Multi-Agent Decision Engine

**A better way to make consequential choices explicit, testable, and revisitable.**

The AI Diplomat convenes four independent AI perspectives, lets the user correct their assumptions, runs a rebuttal round, and asks a Mediator to turn the disagreement into a conditional decision brief.

**Featured specialization: Founder Runway.** It is the deeply guided track for the founder question: _Should I quit my job to build full-time, or earn the right through paid customer proof?_ The same council pattern is also available for Career Move, Relocation, and Open Decision choices.

It does not predict the future or verify external facts. It helps make the next irreversible move smaller, evidence-based, and easier to revisit.

## Decision tracks

| Track | What it supports | What makes it distinct |
| --- | --- | --- |
| **Founder Runway** | Leaving income to build full-time | Deterministic cash-runway and customer-proof gate |
| **Career Move** | A role, offer, field, or study decision | Makes opportunity cost, support, scope, and fallback explicit |
| **Relocation** | Move, stay, defer, or test a city first | Separates belonging and logistics from unverified work, housing, and paperwork facts |
| **Open Decision** | Other non-emergency consequential choices | A values, constraints, evidence, and reversibility record |

Founder Runway is the current hero experience. The other tracks are structured council support, not bespoke expert systems or fact-verification tools.

## What makes it different

- **Four independent voices + one Mediator:** Devil’s Advocate, Optimist, Risk Analyst, and Psychologist debate through distinct lenses before the Mediator synthesizes the brief.
- **Evidence before eloquence:** Every track separates user-reported facts, assumptions, and what must still be verified or tested.
- **Useful disagreement:** Agents state a categorical posture—Cautious, Conditional, or Supportive—not a fake probability of success.
- **Human correction point:** The user edits or removes the council’s assumptions between the independent first round and the rebuttal round.
- **A decision loop:** Every brief ends with a concrete evidence action, a reversibility guardrail, a measurable if/then rule, a downloadable transcript, and an optional calendar check-in export.
- **Honest scripted demos:** Each track has its own fixed, internally consistent example. Demo content is visibly marked as scripted—not personalized model output.

## Founder Runway: the fully guided track

Founder Runway asks for the variables that materially change a pre-quit decision:

- Cash available, personal burn, and committed monthly revenue
- Expected time to a paid pilot and current customer evidence
- Financial responsibilities and a check-in date
- The assumption most likely to break the plan
- A 30-day proof-of-demand threshold

Before the council runs, the app calculates a transparent readiness gate—such as **Protect income**, **Earn the right**, or **Proceed cautiously**—from user-entered numbers. The model explains trade-offs; it does not invent the arithmetic.

## Architecture

~~~mermaid
flowchart LR
  I[Track-specific decision record] --> G{Founder Runway?}
  G -->|Yes| R[Deterministic runway & proof gate]
  G -->|No| E[Evidence & reversibility frame]
  R --> C[Four GPT-5.6 council perspectives]
  E --> C
  C --> H[User corrects assumptions]
  H --> B[Cross-agent rebuttals]
  B --> M[Mediator decision brief]
  M --> O[Decision rule, export, calendar check-in]
~~~

The UI is a dependency-free [index.html](index.html). Live requests go through [api/deliberate.js](api/deliberate.js), a Vercel relay that keeps the OpenAI API key off the client and streams Server-Sent Events to the browser. See the fuller [architecture notes](docs/architecture.md).

## Run it

### Scripted Demo

Open index.html in a modern browser, or serve it locally:

~~~bash
python3 -m http.server 4173
~~~

Select a track, load its matching example, then choose **Deliberate → Use scripted Demo**. The demo always works without an API key and never claims to analyze typed personal details.

### Live GPT-5.6

Live Mode requires a Vercel deployment with an OpenAI API key configured as an environment variable. The browser never asks for, stores, or sends an API key.

1. Import or deploy this repository to Vercel.
2. Add OPENAI_API_KEY in Vercel Environment Variables.
3. Redeploy.
4. Choose **Use Live GPT-5.6** in the app.

The relay only accepts the exact gpt-5.6 model identifier, bounds request sizes and token budgets, forces streaming and store: false, and does not intentionally log deliberation content.

## Evaluation and user learning

This project intentionally does not claim benchmark or usability results that have not been run. The [evaluation protocol](docs/evaluation.md) begins with Founder Runway—the most opinionated track—and provides a controlled comparison with a single-model answer, a blind scoring rubric, and a 3–5 participant usability-study guide.

Before submission, run the protocol, publish only measured results, and add only real participant quotes or outcomes.

## Trust boundaries

- The AI Diplomat is a planning aid, not financial, legal, tax, investment, medical, emergency, crisis, or professional relationship advice.
- It cannot verify salary, offer, tax, visa, housing, funding, market, customer, school, or employer claims. Treat every record as user-provided information and validate material facts separately.
- Scripted Demo stays in the browser. Live Mode sends decision text to the app relay and OpenAI; avoid personal identifiers, confidential customer data, and account information.
- The included relay is a meaningful prototype boundary, not a complete public-scale security program. Authentication, durable rate limiting, budget controls, monitoring, incident response, and a reviewed privacy policy are still required before broad public launch.

## Suggested 90-second demo

1. Open with the founder question: “Do I quit now—or earn the right first?”
2. Load the Founder Runway example and point out the deterministic **Earn the right** gate: six months of runway is not the same as paid demand.
3. Show the assumption-correction checkpoint, rebuttal, and final if/then decision rule.
4. Switch to Career Move or Relocation to show that the same council pattern adapts its evidence frame and decision brief without pretending to know external facts.
5. Export the brief and add the check-in to a calendar.
6. Close with the distinction: this is not five chatbots voting; it is a repeatable decision loop that turns uncertainty into a test.
