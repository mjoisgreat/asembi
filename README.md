# The AI Diplomat — Founder Runway Decision Rehearsal

**Should you quit to build the company now—or earn the right to?**

The AI Diplomat is a structured decision rehearsal for founders facing a high-stakes runway choice. Four specialist perspectives surface the trade-offs; a mediator turns their disagreement into a concrete customer-proof experiment, a stop-loss, and a check-in.

## The founder moment it serves

It is built for decisions such as:

- Quit a job now or keep income while validating demand?
- Build the product or sell a paid pilot first?
- Bring on a cofounder or stay solo?
- Extend runway, raise capital, pivot, or stop?

Rather than pretending to predict a founder’s future, it distinguishes evidence from hope and makes the next irreversible move smaller.

## What makes it different

- Inputs are founder-specific: personal cash runway, monthly burn, financial responsibilities, customer evidence, and a 30-day proof-of-demand target.
- Four agents debate from different lenses: runway protection, growth leverage, founder risk, and founder psychology.
- Users correct the council’s assumptions between the independent round and the rebuttal round.
- The Founder Decision Brief preserves disagreement, compares three paths, and produces a next customer proof, founder stop-loss, and calendar check-in.
- Demo Mode works without an API key; Live Mode streams GPT-5.6 responses in real time.

## Run locally

Open `index.html` in a modern browser. No build step is required.

Use Demo Mode to run without an API key. Live Mode uses GPT-5.6 through the Chat Completions API and keeps the user-provided key only in page memory.

## Evaluation protocol

Compare a normal single-answer model response with an AI Diplomat Founder Decision Brief on these cases:

1. Six months of savings and one interested—but unsigned—B2B lead.
2. A stable job versus quitting to accelerate a product with no revenue.
3. A potential cofounder requesting 40% equity in exchange for sales capability.
4. Three interested prospects, but no commitment: paid pilot versus polished product.
5. A founder with revenue but a shrinking runway who must decide whether to raise, cut costs, or pivot.

Score each output from 0–2 for:

- Cash runway and personal downside made explicit.
- Confirmed customer evidence separated from speculation.
- Material disagreement preserved rather than averaged away.
- Missing evidence identified and made testable.
- A paid validation experiment and explicit stop-loss included.

Do not claim benchmark results until this protocol has been run and documented.

## Safety and privacy

The AI Diplomat is a thinking partner, not financial, legal, tax, medical, investment, emergency, or crisis advice. Live Mode sends the user’s decision text to OpenAI. Avoid sensitive identifiers and verify material facts with qualified professionals.

## Production note

This Build Week prototype intentionally remains a single static HTML file. A public production deployment must move model calls behind a server-side relay with secrets management, authentication, rate limits, cost controls, monitoring, and a full privacy policy.

## Suggested 90-second demo

1. Select **Six months + one lead**.
2. Add the founder’s burn, responsibilities, and a check-in date.
3. Show the independent council perspectives and their evidence requirements.
4. Correct an assumption at the checkpoint.
5. Show the rebuttal and Founder Decision Brief recommending a paid-pilot experiment with a stop-loss.
6. Download the brief or add the review date to a calendar.
