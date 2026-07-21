# The AI Diplomat — Founder Runway Decision Rehearsal

**Should you quit to build the company now—or earn the right to?**

The AI Diplomat is a focused decision rehearsal for founders deciding whether to leave income and build full-time. It turns a vague, high-stakes choice into a visible runway-and-proof gate, a structured council debate, and a conditional customer-validation plan.

It does not predict whether a startup will succeed. It helps a founder make the next irreversible move smaller, testable, and easier to revisit.

## The founder moment it serves

V1 is deliberately narrow:

> **Should I quit my job to build full-time, or preserve income until I have paid customer proof?**

The app asks for the facts that materially change that decision:

- Cash available, personal burn, and committed monthly revenue
- Expected time to a paid pilot
- Customer-evidence stage
- Financial responsibilities and a check-in date
- The assumption most likely to break the plan
- A 30-day proof-of-demand threshold

## What makes it different

- **Founder Readiness Gate:** Calculates net burn and cash runway before any model call, then applies transparent planning gates such as “Protect income,” “Earn the right,” and “Proceed cautiously.”
- **Evidence ledger:** Separates user-reported facts, assumptions, and proof still required. The council is instructed to treat all user text as data, not instructions.
- **Useful disagreement:** Four focused perspectives debate runway protection, growth leverage, founder risk, and founder psychology. The app presents each as a plain-language posture—not a misleading probability.
- **Human correction point:** The founder edits or removes the council’s assumptions between the independent first round and the rebuttal round.
- **Decision loop:** The final brief includes a paid customer proof, a cash/time stop-loss, a clear if/then decision rule, a calendar check-in, and a downloadable transcript.
- **Honest demo:** One scripted, internally consistent pre-quit example works without credentials. It is not presented as a live model result.

## Architecture

~~~mermaid
flowchart LR
  F[Founder inputs] --> G[Deterministic Readiness Gate]
  G --> L[Known / Assumed / Must prove ledger]
  L --> C[Four GPT-5.6 council perspectives]
  C --> H[Founder corrects assumptions]
  H --> R[Cross-agent rebuttals]
  R --> M[Mediator Decision Brief]
  M --> O[Decision rule, export, calendar check-in]
~~~

The UI remains a dependency-free index.html. Live requests go through api/deliberate.js, a Vercel server relay that keeps OPENAI_API_KEY off the client and streams Server-Sent Events to the browser. See the fuller [architecture notes](docs/architecture.md).

## Run it

### Demo mode

Open index.html in a modern browser, or serve it locally:

~~~bash
python3 -m http.server 4173
~~~

Choose **Load worked example**, then **Deliberate → Use scripted Demo**. This shows the complete founder flow without an API key.

### Live GPT-5.6 mode

Live Mode requires a Vercel deployment and an OPENAI_API_KEY environment variable configured in Vercel. The browser never asks for, stores, or sends an API key.

1. Import or deploy this repository to Vercel.
2. Add OPENAI_API_KEY in the Vercel project’s Environment Variables for the intended environment.
3. Redeploy.
4. Choose **Use Live GPT-5.6** in the app.

The relay only accepts the exact gpt-5.6 model identifier, bounds request sizes and token budgets, forces streaming and store: false, and does not intentionally log deliberation content.

## Evaluation and user learning

This project intentionally does not claim benchmark or usability results that have not been run. The [evaluation protocol](docs/evaluation.md) contains:

- Five founder cases for comparing the Decision Brief with a normal single-answer model response
- A blind scoring rubric
- A blank results sheet
- A 3–5 founder usability-study guide

Run the study, publish the actual results, and add only real participant quotes or outcomes before submission.

## Trust boundaries

- The AI Diplomat is a planning aid, not financial, legal, tax, investment, medical, emergency, or crisis advice.
- It cannot verify salary, tax, visa, funding, market, or customer claims. Treat the ledger as user-reported information and validate material facts separately.
- Scripted Demo stays in the browser. Live Mode sends decision text to the app’s relay and OpenAI; avoid personal identifiers, confidential customer data, and account information.
- The included relay is a meaningful prototype boundary, not a complete public-scale security program. Authentication, durable rate limiting, budget controls, monitoring, incident response, and a reviewed privacy policy are still required before broad public launch.

## Suggested 90-second demo

1. Open with the founder question: “Do I quit now—or earn the right first?”
2. Load the worked example and point out the deterministic **Earn the right** gate: six months of runway is not the same as paid demand.
3. Start the scripted council and show the four different evidence requirements.
4. Pause at the assumption review and correct a claim if needed.
5. Show the rebuttal, plain-language disagreement pattern, and final if/then decision rule.
6. Export the brief and add the check-in to a calendar.
7. Close with the distinction: this is not five chatbots voting; it is a repeatable decision loop that turns a founder’s hope into a test.
