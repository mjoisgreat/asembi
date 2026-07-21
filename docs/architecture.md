# Architecture and trust boundary

The deployed application has a dependency-free browser UI plus a small Vercel server function for live GPT-5.6 calls. The server relay keeps the project API key out of the browser; it does not make generated advice verified or production-safe by itself.

## Current request flow

~~~mermaid
flowchart TB
  Founder["Founder in a browser"]
  UI["index.html
  Founder gate, ledger, council UI,
  transcript and calendar exports"]
  Demo["Scripted demo fixtures
  no network request"]
  Relay["Vercel Function
  POST /api/deliberate"]
  Secret["Vercel environment variable
  OPENAI_API_KEY"]
  OpenAI["OpenAI Chat Completions API
  gpt-5.6"]

  Founder --> UI
  UI -->|"Scripted Demo"| Demo
  UI -->|"Live Mode: same-origin JSON"| Relay
  Relay -->|"reads only on server"| Secret
  Relay -->|"validated streaming request"| OpenAI
  OpenAI -->|"SSE chunks"| Relay
  Relay -->|"SSE chunks"| UI
~~~

## Browser application

The interface is intentionally one dependency-free HTML page:

- A deterministic Founder Readiness Gate calculates net burn and cash runway from user-entered figures.
- A Known / Assumed / Must prove ledger makes the trust status of each input visible.
- Four council perspectives run independently, then react to the other first-round positions.
- The founder can correct assumptions before rebuttals.
- The mediator produces a customer-proof experiment, stop-loss, conditional decision rule, alternatives, and a plain-language council pattern.
- Transcript and calendar exports are created locally with Blob URLs. The app does not upload those exports.

Live Mode never asks the founder to paste an OpenAI API key. Scripted Demo has no network call.

## Relay contract

The browser sends a bounded JSON request to POST /api/deliberate. It contains a fixed gpt-5.6 model name, two text messages, a completion budget, optional temperature, and optional JSON-object response format.

The relay:

1. Allows POST with JSON only and rejects oversized or malformed bodies.
2. Accepts only gpt-5.6, supported roles, bounded message count/length, bounded token count, valid temperature, and JSON-object output when requested.
3. Reads OPENAI_API_KEY only from the Vercel server environment. It never accepts or returns a browser-supplied OpenAI key.
4. Forces one streamed upstream response and requests store: false.
5. Forwards the Server-Sent Events stream with cancellation and backpressure handling.
6. Uses generic errors and does not intentionally log deliberation content or credentials.

The browser parses each SSE chunk, appends delta content as it arrives, and advances to the next agent only when the prior stream is complete. The mediator also uses the relay stream, then parses its JSON-object response locally.

## Data and privacy boundary

| Topic | Current behavior | Important limitation |
| --- | --- | --- |
| API key | Held only in Vercel environment variables | The owner must configure OPENAI_API_KEY for each intended Vercel environment |
| Founder decision text | In Live Mode: browser → relay → OpenAI | The app asks users to avoid identifiers and confidential customer data; platform/provider retention policies still matter |
| Demo text | Embedded in the browser | It is fixed demonstration copy, not model output |
| App database | None | This does not remove Vercel platform logs or OpenAI API data handling from the privacy picture |
| Exports | Created locally in the browser | The user decides whether to save, share, or delete them |
| Recommendation | Generated from user-provided facts and model reasoning | It cannot verify salary, tax, visa, funding, market, or customer claims |

The relay protects a project secret. It does not establish the truth of the recommendation, authenticate a user, or provide a complete privacy program.

## Controls implemented

- [x] Same-origin Vercel relay at /api/deliberate
- [x] Server-only OPENAI_API_KEY access
- [x] Exact model allowlist and request/message/token bounds
- [x] Forced SSE, store: false, cancellation, and backpressure handling
- [x] Browser migration away from direct OpenAI calls and browser API-key entry
- [x] Deterministic intake gate and user-reported evidence ledger
- [x] Generic failures without deliberate-content logging in the route
- [x] Basic response headers for content type, referrer, and unused browser permissions

## Before a public launch

- [ ] Configure OPENAI_API_KEY in Vercel and test the live service in every target environment.
- [ ] Add authentication or a deliberately constrained anonymous-use policy.
- [ ] Add durable per-user and per-IP rate limits, concurrency caps, session/request IDs, and spend alerts. In-memory counters alone are not adequate across serverless instances.
- [ ] Enforce the permitted council round sequence server-side and set output-size/time limits.
- [ ] Add an explicit output-safety policy and test malformed streams, upstream 429s, timeouts, cancellations, and policy refusals.
- [ ] Publish a reviewed privacy policy that identifies processors, retention, deletion, and contact paths.
- [ ] Add operational monitoring, incident response, and a tested key-rotation procedure.

## Design principle

The deterministic gate owns transparent arithmetic and threshold logic. The model is used to expose trade-offs, challenge assumptions, and synthesize a testable plan—not to invent financial certainty or turn agent agreement into a forecast probability.
