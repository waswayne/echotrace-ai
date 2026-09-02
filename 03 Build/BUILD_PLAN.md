# EchoTrace Build Plan

Status: planning only; coding has not been approved.

## Demo Goal

- User can narrate a fictional near miss by voice, clarify a missing fact,
  correct a possible discrepancy, interrupt a mistaken read-back, and review a
  source-linked timeline.
- Core outcome: a structured account that visibly preserves what was said,
  what changed, what remains unknown, and what the speaker confirmed.
- Success check: the complete value proposition is understandable in under
  three minutes.

## Must Have

- [ ] Explicit consent and non-emergency notice.
- [ ] Temporary-token browser authentication.
- [ ] Live AssemblyAI voice session.
- [ ] Final transcript turns with stable provider identifiers.
- [ ] Interruption and barge-in handling.
- [ ] Application-owned interview state.
- [ ] Schema-validated source-linked claims.
- [ ] Provisional timeline and explicit unknowns.
- [ ] One neutral missing-information question.
- [ ] One possible discrepancy and correction history.
- [ ] Final speaker review.

## Nice To Have

- [ ] Minimal saved fictional cases.
- [ ] User-controlled deletion.
- [ ] Draft structured-account download.
- [ ] Additional language after English is reliable.

## Explicitly Out Of Scope

- Multiple witnesses and cross-account analysis.
- Truth, lie, deception, credibility, liability, or severity scores.
- Emergency response or live operational dispatch.
- Automatic filing, emails, notifications, or work orders.
- Legal, insurance, HR, medical, or regulatory decisions.
- Telephony, offline mode, RAG, vector search, and multi-agent systems.
- Production identity, organizations, billing, and broad integrations.

## Proposed Stack - Not Installed

- Next.js, React, and TypeScript.
- AssemblyAI managed Voice Agent API.
- Server-side temporary-token route and direct browser WebSocket.
- Zod for runtime validation.
- In-memory state for milestone one.
- Supabase PostgreSQL only after the golden path works.
- Tailwind CSS with a small accessible component set.
- Vitest, React Testing Library, and Playwright.
- Vercel deployment.
- Optional AssemblyAI LLM Gateway for schema-constrained classification.

No setup, test, or demo commands exist until the application is initialized
after explicit approval.

## Delivery Sequence

### Phase 0 - Current: Approval And Rules

- Confirm niche, scope, consent, retention, language, deployment, and spending.
- Close or explicitly accept every unresolved hackathon-rule risk.
- Freeze the fictional scenario and evaluation rubric.

### Phase 1 - Voice Vertical Slice

- Temporary token.
- Live managed voice connection.
- Three finalized user turns.
- Agent follow-up and interruption behavior.
- One claim card linked to its source turn.
- No database and no discrepancy engine.

### Phase 2 - Structured State

- Claims, source spans, timeline events, gaps, and revisions.
- Runtime schemas and invalid-output handling.
- Ten synthetic scenario variations.

### Phase 3 - Clarification And Correction

- Deterministic discrepancy candidates.
- Optional structured classification.
- Neutral questions, decline path, corrections, and final review.

### Phase 4 - Reliability And Demo

- Consent, deletion, microphone, network, and reconnect behavior.
- Accent, noise, pause, interruption, and latency testing.
- Clean-browser deployment test.
- Feature freeze, video, pitch, limitations, and backup path.

## Target Milestones

Dates depend on prompt approval to start coding.

| Milestone | Target | Status |
| --- | --- | --- |
| Scope and rules gate | 2026-09-03 | Awaiting approval |
| Voice vertical slice | 2026-09-07 | Not started |
| Structured state | 2026-09-14 | Not started |
| Clarification and review | 2026-09-21 | Not started |
| Feature-frozen demo | 2026-09-25 | Not started |
| Submission candidate | 2026-09-28 | Not started |

## First Implementation Milestone Acceptance Criteria

- Permanent AssemblyAI key is not present in browser code or repository files.
- Browser obtains a short-lived token from the server.
- User completes at least three natural spoken turns.
- Final transcript events appear with their source identifiers.
- The agent asks one short follow-up.
- The user interrupts and queued agent playback stops correctly.
- One validated claim card links to its exact source turn.
- Session ends cleanly and microphone/connection errors are understandable.
- No database, authentication system, or discrepancy engine is added.

## Testing Principles

- Test observed behavior, not model intent.
- Use fictional data only.
- Include ambiguous time, unknown answer, correction, refusal, interruption,
  invalid tool payload, microphone denial, and lost-connection cases.
- Never publish accuracy percentages without a documented test set and method.
