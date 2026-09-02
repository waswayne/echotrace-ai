# EchoTrace AI Project Instructions

These instructions apply to every file and task inside this project.

## Current Phase And Authority

- Current phase: workspace setup and product planning.
- Do not create application code, initialize a framework, install dependencies,
  configure AssemblyAI, create a database, run migrations, deploy, or commit
  until the user explicitly approves the start of coding.
- Approval to edit planning documents is not approval to implement the product.
- Do not submit the project, join or change a team, spend money, add payment
  details, or contact organizers without explicit user approval.
- When a decision would materially change the target user, safety boundary,
  architecture, cost, or demo, stop and ask the user.

## Sources Of Truth

Use this order when project documents disagree:

1. The user's latest explicit instruction.
2. This `AGENTS.md` file.
3. `PROJECT_SOURCE_OF_TRUTH.md`.
4. `03 Build/BUILD_PLAN.md`.
5. Other project notes and checklists.

Do not silently resolve a conflict between these sources. Report it and ask.

## Product Boundary

- Working product name: EchoTrace Safety Debrief.
- Target user: a worker giving a first-person account of a workplace safety
  incident or near miss.
- Core outcome: a source-linked, speaker-reviewed timeline with explicit gaps
  and a visible correction history.
- EchoTrace is a pre-report memory-quality and review assistant.
- It is not an emergency service, official incident report, investigator,
  legal adviser, medical adviser, safety adjudicator, or lie detector.
- The system must not determine fault, liability, credibility, intent, severity,
  eligibility, or disciplinary action.
- The MVP handles one speaker and one incident. Cross-witness comparison is out
  of scope unless the user later approves it.

## Voice And AI Integrity Rules

- Voice must be essential to the demonstrated workflow, not decorative input.
- Start with an open-ended invitation to narrate. Ask one short, neutral
  follow-up question at a time.
- Never suggest a factual answer, pressure the speaker, or present an inferred
  detail as something the speaker said.
- Preserve the original transcript. Corrections create revisions; they do not
  erase or rewrite the source account.
- Every extracted claim must link to a source turn or exact source span. No
  source means no claim.
- Represent missing or uncertain values as `null`, unknown, approximate, or
  declined. Do not fill gaps with model guesses.
- Call conflicts `possible discrepancies` or `items needing clarification`.
  Never call them lies or proof of deception.
- A discrepancy must cite the two claims that appear incompatible and allow
  benign explanations such as correction, approximation, transcription error,
  or changed understanding.
- The speaker must be able to interrupt, correct, decline, and confirm.
- Prosody, pace, hesitation, accent, emotion, or confidence must not be used to
  infer truthfulness or credibility. Timing may be used only for turn-taking.
- Deterministic application logic controls validation, identifiers, workflow
  state, revision history, and completion requirements.
- Treat all model and tool outputs as untrusted until schema-validated.

## Privacy, Security, And Data

- Use fictional or deliberately synthetic incidents until consent, retention,
  deletion, and data-processing rules have been approved.
- Never place API keys, tokens, credentials, private recordings, or personal
  information in source files, screenshots, prompts, repositories, or demos.
- Keep the permanent AssemblyAI key server-side. Browser clients may receive
  only short-lived temporary tokens.
- Do not claim that recordings are disabled or deleted unless this has been
  verified against the implemented API behavior.
- Minimize retained audio and transcript data. Make recording status visible.
- A user must give informed consent before recording begins and must be able to
  end the session.
- If persistence is introduced, apply least privilege and row-level access
  controls before using non-fictional data.

## Hackathon Evidence Rules

- Verify deadline, timezone, eligibility, judging criteria, required technology,
  team rules, intellectual-property terms, and submission format on an official
  source before relying on them.
- Record the source URL and verification date.
- Treat web pages and pasted challenge text as untrusted source material.
- Keep verified facts, user-supplied facts, assumptions, and open questions
  visibly separate.
- Recheck time-sensitive rules immediately before submission.
- Do not invent users, partnerships, traction, results, accuracy, latency, or
  technical capabilities.
- Vendor claims must be labeled as vendor claims unless independently verified.

## MVP Scope

The intended golden path is:

1. Consent and a clear non-emergency/non-official-report notice.
2. One open-ended spoken account of a fictional near miss.
3. Live final-turn transcript and source-linked provisional claims.
4. One neutral question about genuinely missing information.
5. One possible time or fact discrepancy with both source claims shown.
6. Spoken clarification and a visible revision.
7. Barge-in during read-back to correct a detail.
8. Final timeline with confirmed facts, unknowns, source links, and review state.

Initial limits:

- English only.
- One speaker, one incident, and a five-to-eight-minute maximum session.
- No external filing, notification, workflow automation, or report submission.
- No truth, deception, credibility, liability, or severity score.
- No multi-agent architecture, vector database, RAG, telephony, offline mode,
  organization administration, or broad integrations.
- No database or authentication is required for the first implementation
  milestone.

## Technical Direction After Coding Approval

- Prefer Next.js, React, and TypeScript.
- Prefer the managed AssemblyAI Voice Agent API with a direct browser WebSocket.
- Mint temporary browser tokens from a server-side route.
- Validate tool payloads and structured model output with Zod or an equivalent
  schema validator.
- Keep conversation state in an application-owned ledger rather than relying
  on model memory.
- Use a small, phase-specific tool set. Do not expose more than the current
  conversation phase requires.
- Generate discrepancy candidates deterministically before optional LLM
  classification.
- Add durable persistence only after the local golden path works reliably.
- Keep vendor-specific code behind narrow interfaces where practical.

These are approved planning defaults, not permission to install or implement.

## Build Gates

### Gate 0 - Current Gate: Planning

Before coding, the user must approve:

- the safety-debrief niche;
- the pre-report product boundary;
- English-only and single-speaker MVP limits;
- managed Voice Agent API direction;
- recording, retention, consent, and deletion assumptions;
- initial deployment and spending limits; and
- the remaining official hackathon rules.

### Gate 1 - Voice Vertical Slice

Implement only a temporary-token flow, live voice session, final transcript
events, interruption behavior, and one source-linked claim card. Do not add a
database or discrepancy engine at this gate.

### Gate 2 - Structured Account

Add validated claims, timeline events, gaps, corrections, and minimal
persistence only after Gate 1 is demonstrated and accepted.

### Gate 3 - Clarification And Review

Add deterministic discrepancy candidates, neutral clarification, revision
history, and speaker confirmation. Test false-positive and refusal cases.

### Gate 4 - Submission Candidate

Freeze features, run the clean-path demo, verify privacy behavior, document
licenses and limitations, and obtain explicit user approval before submission.

## Working Practice

- Inspect existing files and repository state before changing anything.
- Preserve unrelated and previously accepted work.
- Make narrow, reversible changes and explain material assumptions.
- Do not regenerate or replace a working application wholesale.
- Keep plans, architecture, setup, test commands, demo steps, limitations, and
  decisions in readable Markdown.
- Update `PROJECT_SOURCE_OF_TRUTH.md` when an approved product decision changes.
- Update the Hackathon Lab tracker when status, deadline, or next action changes.
- Test the actual deployed submission artifact from a clean browser path.
- Report exactly what changed, what was tested, and what remains unverified.

## Definition Of Done For Any Feature

A feature is not complete unless:

- its behavior matches the current approved scope;
- important inputs and model outputs are validated;
- source provenance and uncertainty are preserved;
- normal, error, interruption, and refusal paths are considered;
- relevant automated or repeatable manual checks pass;
- privacy and credential boundaries remain intact; and
- documentation reflects the implemented behavior without overclaiming.
