# EchoTrace AI - Product Source Of Truth

Last updated: 2026-09-02

Status: Proposed product direction approved for workspace planning; implementation
requires a separate explicit user approval.

## 1. Product Decision

### Working Name

EchoTrace Safety Debrief

### Target User

A worker who needs to recount a workplace safety incident or near miss soon
after it occurred, especially when speaking is faster and more natural than
typing into a form.

### Core Promise

Turn a worker's spoken recall into a source-linked, speaker-confirmed timeline
with explicit unknowns and a visible correction history before a formal incident
report is filed.

### Product Category

Pre-report memory-quality and review assistant.

### Not The Product

- Not an emergency reporting channel.
- Not an official incident report or system of record.
- Not a lie detector or witness-credibility evaluator.
- Not an investigator or replacement for a trained safety professional.
- Not legal, medical, employment, insurance, or compliance advice.
- Not an autonomous filing, escalation, notification, or disciplinary system.

## 2. Problem

Immediately after an incident, a worker may remember events out of order, omit
basic context, use approximate times, or correct themselves later. Traditional
forms force early structure and can lose the natural narrative. Ordinary voice
recorders preserve audio but do not help the speaker notice missing or unclear
details before handing the account to someone else.

EchoTrace should preserve the original spoken account, structure only what is
supported, and let the speaker resolve ambiguity without being accused or led.

## 3. Why Voice Is Fundamental

Voice is central when the user is on site, moving, stressed, wearing gloves, or
able to remember more through uninterrupted narration than through a form.

The voice-specific behaviors are:

- sustained natural narration;
- semantic end-of-turn handling through pauses;
- one-question-at-a-time clarification;
- immediate spoken corrections;
- barge-in when the agent reads something back incorrectly; and
- low-friction capture close to the event.

Timeline extraction and discrepancy checking alone are not voice-specific. The
product must visibly demonstrate the narration, interruption, and spoken
confirmation loop to justify being a voice application.

Prosody is used only for turn-taking. It is never evidence of deception,
credibility, intent, or emotional state.

## 4. Golden-Path Demo

Use a fictional warehouse forklift near miss.

1. The worker sees a consent notice and confirms that the situation is not an
   active emergency.
2. EchoTrace asks: "Tell me what happened from the beginning, in your own words."
3. The worker gives a natural account. Final transcript turns and provisional
   source-linked claims appear.
4. EchoTrace notices a truly missing fact and asks one neutral question.
5. A later answer creates a possible time discrepancy with an earlier claim.
6. EchoTrace shows both source excerpts and asks the worker to clarify without
   suggesting which answer is correct.
7. The worker corrects the timeline. The original claim remains visible and a
   revision is recorded.
8. EchoTrace reads back a summary. The worker interrupts to correct one detail.
9. The final view shows confirmed events, unresolved unknowns, sources,
   revisions, and a "reviewed by speaker" state.

Target demonstration time: two to three minutes.

## 5. MVP Functional Requirements

### Consent And Session

- Explain recording and processing before microphone capture begins.
- State that EchoTrace is not an emergency service or official report.
- Allow the user to stop the session at any time.
- Show listening, thinking, speaking, interrupted, reconnecting, and error states.

### Conversation

- Begin with an open-ended narrative prompt.
- Ask one short, neutral question at a time.
- Permit interruptions and spoken corrections.
- Permit unknown, approximate, declined, and uncertain answers.

### Structured Account

- Capture claims only from final user transcript turns.
- Link every claim to a source turn or exact source excerpt.
- Construct provisional timeline events from supported claims.
- Track missing information separately from possible discrepancies.
- Preserve the original claim when a correction creates a new revision.

### Clarification

- Generate discrepancy candidates from claims about the same event or attribute.
- Show the exact competing claims.
- Classify candidates as conflict, update, uncertainty, transcription issue, or
  compatible approximation where possible.
- Ask a neutral reconciliation question only when useful.
- Let the speaker decline to resolve the issue.

### Review

- Show confirmed, provisional, corrected, and unresolved information.
- Show source excerpts and revision history.
- Require an explicit speaker-review action.
- Export or external filing is not required for the MVP.

## 6. Non-Functional Requirements

- The conversation should remain usable under ordinary network latency.
- Agent replies should be concise enough to preserve conversational pace.
- Tool and model payloads must be schema-validated.
- The application must recover gracefully from microphone denial, connection
  loss, interrupted replies, invalid tool arguments, and unavailable services.
- Credentials must never reach the client or repository.
- The demo must use fictional data and work from a clean browser path.
- Product claims must reflect observed behavior, not planned capability.

## 7. Initial Scope

### Must Have

- Direct browser voice session using AssemblyAI.
- Final-turn transcript display.
- Semantic turn-taking and barge-in behavior.
- Application-owned conversation state.
- Source-linked claims and provisional timeline.
- One missing-information clarification.
- One possible discrepancy and correction loop.
- Final review with unknowns and revision history.

### Nice To Have After The Golden Path

- Minimal saved fictional cases.
- Session replay for debugging.
- A user-controlled deletion action.
- Downloadable structured account marked as a draft.
- Carefully tested support for an additional language.

### Explicitly Out Of Scope

- Multiple witnesses or cross-account comparison.
- Truth, lie, credibility, fault, liability, or severity scoring.
- Emergency dispatch or live safety monitoring.
- Automatic report filing, emails, notifications, or work orders.
- Legal, insurance, HR, medical, or regulatory conclusions.
- Telephony, native mobile application, or offline speech processing.
- RAG, vector databases, multi-agent orchestration, and broad integrations.
- Production organization management, billing, and enterprise authentication.

## 8. Proposed Architecture

This is a planning decision, not permission to implement.

1. A Next.js/React browser interface captures microphone audio and displays the
   live conversation, evidence ledger, timeline, and review state.
2. A server-side route uses the permanent AssemblyAI key to mint a short-lived
   browser token.
3. The browser connects directly to the managed AssemblyAI Voice Agent API over
   WebSocket.
4. Transcript and tool events update an application-owned state engine.
5. Tool parameters and structured model output are validated with JSON Schema
   and Zod or an equivalent runtime validator.
6. Deterministic rules generate possible discrepancy candidates.
7. An optional structured LLM call classifies a candidate but cannot create or
   alter its source evidence.
8. Persistence is added only after the in-memory golden path works. Supabase
   PostgreSQL is the current candidate.

### Proposed Conversation States

- `consent`
- `open_narrative`
- `claim_capture`
- `gap_clarification`
- `discrepancy_clarification`
- `read_back`
- `final_review`
- `ended`

### Proposed Tool Set

- `capture_claims`
- `record_gap`
- `propose_clarification`
- `apply_user_correction`
- `finalize_account`

Expose only tools appropriate to the current conversation state.

## 9. Core Data Model

- `Case`: ID, domain, status, creation time, consent state.
- `VoiceSession`: case ID, AssemblyAI session ID, language, start/end times,
  recording policy.
- `Turn`: session ID, provider turn/item ID, speaker, transcript, confidence,
  and timestamps.
- `SourceSpan`: turn ID, exact excerpt, character boundaries, available timing.
- `Claim`: subject, predicate, value, normalized value, temporal anchor,
  location, certainty, status, and source span.
- `TimelineEvent`: event type, approximate or exact time range, linked claim IDs.
- `Gap`: topic, reason, priority, and open/resolved/declined state.
- `Discrepancy`: two claim IDs, type, alternative explanations, and state.
- `Clarification`: linked gap or discrepancy, neutral question, answer turn, and
  resolution.
- `Revision`: entity, previous value, new value, actor, source turn, timestamp.
- `Review`: speaker-confirmed state, confirmation time, unresolved items.

Forbidden fields include truth score, lie score, deception score, and
credibility score.

## 10. Reliability And Safety Strategy

- No source, no claim.
- Open-ended recall precedes targeted questions.
- Missing information is not a discrepancy.
- A discrepancy is a candidate until the speaker reviews it.
- Preserve uncertainty rather than converting it into false precision.
- Validate all AI-generated structures at runtime.
- Keep the raw transcript and revisions available for review.
- Use synthetic scenarios until the data policy is approved.
- Save finalized turns incrementally once persistence exists.
- Keep sessions short and replies concise to control latency and cost.

## 11. Success Measures

### Demo Success

A judge understands the complete value proposition in under three minutes and
sees voice narration, a source-linked claim, a gap, a possible discrepancy, a
spoken correction, interruption handling, and a final review.

### MVP Quality Checks

- Every visible claim has a valid source.
- Unsupported details remain absent or unknown.
- The scripted discrepancy can be resolved without a leading question.
- An interrupted reply stops cleanly.
- The user can decline a question without blocking completion.
- The final account distinguishes confirmed, corrected, and unresolved items.

Do not invent accuracy percentages before a documented evaluation exists.

## 12. Judging-Criteria Map

- Application of technology: real-time AssemblyAI voice, turn handling,
  interruptions, tool calls, and transcript provenance drive the workflow.
- Presentation: one fictional, repeatable warehouse scenario with a visible
  transformation from speech to reviewed account.
- Business value: safer, faster preparation of incident recollections before
  formal reporting.
- Originality: speaker-controlled correction integrity rather than generic
  transcription, workflow automation, or automated truth judgment.

The criteria above came from the user-supplied event brief and still need to be
verified against an event-specific official rules source.

## 13. Competitive Boundary

EchoTrace must not position itself as generic field reporting. Current event
projects and commercial products already cover voice-to-work-order, field-report
structuring, live incident intelligence, compliance intake, and insurance claim
interviews.

The differentiator is the single speaker's pre-report clarification process:

- source-linked claims;
- explicit unknowns;
- neutral discrepancy resolution;
- preserved correction history; and
- speaker confirmation without credibility judgment.

This is a focused wedge, not uncontested market whitespace.

## 14. Approved Planning Defaults

- Solo project.
- English-only MVP.
- One speaker and one incident.
- Managed AssemblyAI Voice Agent API.
- Next.js, React, TypeScript, and runtime schema validation.
- In-memory first milestone; optional Supabase later.
- Fictional warehouse demo data.
- Two-to-three-minute presentation path.
- No external actions or formal report submission.

These defaults remain subject to user approval before coding.

## 15. Open Decisions

- Final approval of the safety near-miss niche.
- Whether the product may retain any audio.
- Required deletion behavior and acceptable retention period.
- Whether the first demo needs persistence.
- Deployment account and maximum permitted spend.
- Event-specific team-size rules.
- Event-specific intellectual-property and license terms.
- Exact required submission assets and repository visibility.
- Final confirmation of judging criteria.

## 16. Change Control

When an approved decision changes:

1. Update this document and record the date.
2. Update any affected tracked build or demo documentation.
3. Explain any impact on scope, safety, schedule, and cost.
4. Preserve superseded major plans in the local Hackathon Lab archive when
   traceability matters; do not republish private planning material by default.
5. Do not silently broaden the MVP.
