# DiamondRide repository instructions

DiamondRide is a lightweight mountain-bike route planning and pre-ride visual screening prototype. The implementation must remain structurally sound for future commercialization without requiring a self-hosted GPU.

## Architecture
- Frontend: React/JavaScript; browser geolocation only with user permission; map display separate from route generation.
- Backend: FastAPI coordinates API calls, auth, validation, and responses.
- Data: Supabase/PostGIS for trail information, condition reports, feedback, and user data where needed.
- Routing: an external routing/trail service generates candidate routes; do not invent route geometry or safety data.
- ML: a small CPU-compatible model may score rider-perceived difficulty or trail conditions once validated training data exists. Use rules for known closures, access restrictions, and hard experience constraints.
- Vision: hosted inference behind a provider interface; never depend on a local GPU or expose service keys in frontend code. Treat bike photos as preliminary observations, not mechanical safety certification.
- LLM: optional for explanations based on verified data, never the source of route facts.

## Non-negotiable code standards
- Implement only explicitly requested features and changes. Do not add speculative frameworks, agents, screens, packages, or configuration.
- Preserve existing interfaces and behavior unless the task explicitly requires changing them.
- Before coding, inspect the relevant files and reuse established patterns; choose the smallest coherent change.
- Every specifically named function, endpoint, or component must be implemented with its requested signature/contract unless blocked; identify blockers explicitly.
- Prefer plain functions over classes unless shared state, polymorphism, or existing conventions justify classes.
- Avoid duplicate logic, redundant wrappers, giant files, unrelated refactors, verbose comments, unnecessary try/except, and silent fallbacks.
- Do not shorten code at the expense of readability, input validation, or correct error handling. No arbitrary line count limits.
- Keep business logic separate from provider adapters. Keep external service calls isolated for testing and replacement.
- Use Pydantic schemas for FastAPI boundaries. Validate external responses; set timeouts and handle failures explicitly.
- Never fabricate API responses, ML accuracy, trail conditions, risk probabilities, or completed functionality. Test doubles belong only in tests.
- Do not store uploaded images or precise location histories by default. Minimize data collection, keep secrets server-side, and follow least-privilege access.

## Execution and verification
- For tasks with multiple requirements, create a short acceptance checklist mapping each requirement to code and test evidence before editing.
- Make focused changes, then run relevant existing tests and lint/type checks if configured; add small targeted tests for newly requested behavior.
- Do not claim completion if code is unimplemented, tests were not run, or integrations could not be verified. State exact limitations.
- Finish with: changed files, requirements implemented, tests run/results, and any remaining blockers. Keep this concise.

For feature implementation and review, use the `diamondride-engineering` skill in `.agents/skills/diamondride-engineering/SKILL.md`.


# Codex Efficiency Rules

## Agent delegation
- Complete tasks using the primary agent by default.
- Do not spawn subagents for routine edits, debugging,
  file discovery, or simple research.
- Delegate only when independent workstreams provide
  a clear benefit.
- Never spawn multiple agents to investigate the
  same question.
- Do not create subagents just to summarize results.

## Code exploration
- Inspect the smallest relevant portion of the codebase.
- Use targeted searches before reading entire files.
- Avoid repeatedly reading unchanged files.
- Exclude generated files, virtual environments,
  dependencies, build outputs, and binary files
  unless they are directly relevant.
- Prefer concise command outputs over full logs.
- Avoid dumping entire files into conversation context.

## Implementation
- Make focused changes that solve the requested task.
- Reuse existing utilities instead of creating new ones.
- Avoid unrelated refactoring.
- Do not generate large explanations unless requested.
- Do not repeatedly re-explain established context.

## Testing
- Run the smallest relevant test first.
- Escalate to broader tests only when warranted.
- When tests fail, inspect relevant failure output,
  not the entire log.
- Do not rerun unchanged failing commands repeatedly.

## Reasoning and context
- Use straightforward approaches for simple tasks.
- Preserve useful context for related work.
- Do not compact or restart sessions automatically.
- Summarize findings concisely when exploration ends.
- Report blockers and uncertainty rather than
  repeatedly guessing.

## Quality
- Never sacrifice correctness or security to save tokens.
- Verify material changes.
- Ask before destructive or high-impact operations.
