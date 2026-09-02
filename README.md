# AssemblyAI Voice Agent Hackathon - EchoTrace AI

- Created: 2026-09-02
- Deadline: 2026-09-30 at 15:00 UTC / 16:00 WAT
- Official source: https://lablab.ai/ai-hackathons/assemblyai-voice-agent-hackathon
- Research verified: 2026-09-02
- Status: Planning - workspace ready; coding not yet approved
- Owner: Solo project
- Working product: EchoTrace Safety Debrief
- Next decision: Approve the product boundary and pre-coding gates.

## Product In One Sentence

EchoTrace is a voice-first safety debrief assistant that converts one worker's
spoken recollection of an incident or near miss into a source-linked,
speaker-reviewed timeline with explicit unknowns and correction history.

## Important Boundary

EchoTrace supports a person in clarifying their own account before formal
reporting. It does not determine truth, fault, liability, credibility, severity,
or disciplinary action, and it does not automatically file or send a report.

## Current State

- Discovery and competitor research: complete.
- Workspace and AI operating instructions: complete.
- Exact niche and guardrails: recommended; awaiting user confirmation.
- Application implementation: not started.
- AssemblyAI configuration: not started.
- Dependencies, database, authentication, and deployment: not started.

Open `PROJECT_SOURCE_OF_TRUTH.md` for the full product and technical plan. Any AI
working in this folder must read `AGENTS.md` and that source-of-truth file before
taking action.

## Repository Layout

- `AGENTS.md`: mandatory instructions for AI-assisted work.
- `PROJECT_SOURCE_OF_TRUTH.md`: approved product, safety, architecture, and scope
  decisions.
- `README.md`: public project overview and current status.
- Application files will be created at the repository root after coding is
  explicitly approved.

The numbered Hackathon Lab planning folders are retained locally for project
management but intentionally excluded from the public GitHub repository.

## Before Coding

The user must approve the niche, product boundary, language and speaker limits,
recording/retention policy, managed AssemblyAI approach, spending limit, and
remaining event-specific rules. Planning-document edits do not cross this gate.
