# AGENTS.md

This repository is for a configurable multiplayer journey game built with TypeScript, Expo, and React Native.

The initial theme is Oregon Trail-inspired, but the project should be treated as a reusable journey/adventure engine rather than a one-off clone.

## Project Intent

When contributing to this repo, optimize for these priorities:

1. Preserve configurability.
2. Keep the game engine broader than a single campaign.
3. Support 1 to 5 player multiplayer as a first-class concern.
4. Treat AI as optional, bounded, and replaceable.
5. Design with future encryption in mind without overbuilding v1.

## Product Boundaries

Current in-scope direction:

- party-based trail or route progression
- configurable landmarks, events, stores, branches, and endings
- adjustable time flow and pacing
- resource management and survival decisions
- async/checkpoint multiplayer first
- retro 80s/90s visual direction

Current out-of-scope for first implementation unless explicitly requested:

- full real-time multiplayer
- Signal-protocol integration
- unrestricted AI control of the game economy or progression
- settlement/ranch/descendant systems as a required v1 feature

## Architecture Preferences

- Prefer config-driven systems over hardcoded story logic.
- Keep content packs and rule packs separate.
- Model public party state separately from private player state.
- Ensure the game remains playable without AI services.
- Add extension points for richer AI orchestration later, but do not force it into early milestones.
- Avoid coupling the engine to Oregon-specific names or assumptions when a generic abstraction is cleaner.

## Documentation Rules

When updating docs:

- Keep the distinction clear between `v1`, `future roadmap`, and `open research`.
- Record assumptions explicitly instead of burying them in prose.
- Use checklists in `TODO.md` for backlog items.
- Keep `README.md` focused on product framing and project direction.
- Put implementation backlog and unanswered product questions in `TODO.md`.

## Code Guidance

When code is added:

- Use TypeScript throughout unless there is a strong platform-specific reason not to.
- Favor small, testable modules around game rules, config validation, and state transitions.
- Keep AI interfaces schema-first and validation-heavy.
- Design networking/state interfaces so encrypted transport can be added later.
- Do not hardcode campaign content that should live in config.

## Design Guidance

- Aim for a deliberate retro game feel, not generic app UI.
- Prefer strong map, panel, inventory, and encounter metaphors over feed-like layouts.
- Keep mobile ergonomics in mind from the start.
- Preserve readability and accessibility even with retro styling.

## Collaboration Notes

- If a request conflicts with the config-first direction, call it out before implementing.
- If a feature pushes the project toward a different genre, frame it as either:
  - an engine extension
  - a campaign/content pack
  - a future pillar outside v1
- Treat "AI decides things" as a product tool, not a replacement for core game design.
