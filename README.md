# vibes-oregon-trail

`vibes-oregon-trail` is a planned TypeScript game built with Expo and React Native.

The project starts as a configurable trail-journey simulator inspired by Oregon Trail, then grows into a reusable adventure engine where routes, landmarks, stores, events, pacing, and win conditions can all be changed without rewriting the app.

## Vision

Build a multiplayer journey game where a party of up to 5 players travels together, manages scarce resources, hits narrative checkpoints, and makes hard tradeoffs under pressure.

The long-term goal is not just "Oregon Trail in React Native." The goal is a data-driven engine that can support:

- Oregon Trail-style westward journeys
- Alternate historical or fictional campaigns
- More open-ended choose-your-own-adventure structures
- Later expansions such as settlement play, descendants, ranching, or adjacent simulation layers

## Product Direction

The first playable version should optimize for:

- A clear wagon-travel gameplay loop
- Configurable landmarks, route branches, stores, and random events
- Async/shared-phase multiplayer for 1 to 5 players
- Retro 80s/90s-inspired visuals with readable modern UX
- Optional AI-assisted runtime content inside strict guardrails

The project should avoid hardcoding the game to one specific campaign shape. "Oregon Trail" is the launch theme, not the permanent engine boundary.

## Core Pillars

### 1. Config-first gameplay

Content and core rules should be driven by data wherever practical.

Examples:

- Landmarks and checkpoints
- Travel routes and branching paths
- Stores and item inventories
- Encounters and random events
- Time progression and pacing
- Victory, failure, and ending states

This is important because the same engine may later support very different campaigns.

### 2. Multiplayer by design

The game should support 1 to 5 players in a shared party.

Initial multiplayer target:

- Async or checkpoint-based shared decision making
- Clear ownership of private vs shared state
- Clean upgrade path to live co-op later

### 3. AI as a bounded game master

AI should help generate or vary runtime content such as:

- Store inventories
- Event variations
- Route twists
- Flavor text
- NPC or encounter framing

AI should not be treated as unrestricted authority over the game. Generated output must stay inside schemas, economy limits, rarity rules, and safety constraints. The game must remain playable with deterministic fallback content when AI is disabled or unavailable.

### 4. Encryption-aware architecture

The project may eventually include end-to-end encrypted communications or state sync. Signal integration is a research topic, not a first milestone requirement.

For now, the architecture should be designed so that:

- private player data can be separated from party-visible state
- future encrypted transport is possible without redesigning the entire app
- security decisions are intentional instead of bolted on later

## Visual Direction

The target presentation is a 16-bit homage with strong late-80s/early-90s energy:

- pixel-art-inspired maps and encounters
- chunky simulation UI panels
- readable inventory and party dashboards
- stylized route maps and landmark scenes

The app should feel game-like and specific, not like a generic mobile dashboard with a retro skin pasted on top.

## Near-Term Scope

The first implementation phase should cover:

- project setup in Expo + React Native + TypeScript
- a small playable journey loop
- configurable content packs and rule packs
- a seed Oregon Trail campaign
- async multiplayer foundations
- AI integration boundaries and deterministic fallbacks

Ideas intentionally deferred to later phases:

- full real-time multiplayer
- settlement management as a major system
- descendant/family continuation as core gameplay
- deep economy simulation beyond what the trail loop needs
- Signal-protocol integration

## Suggested Initial Architecture

High-level system boundaries to preserve as the project grows:

- `ScenarioPack`: landmarks, routes, stores, events, endings, presentation metadata
- `RulePack`: pacing, survival tuning, economy knobs, AI permissions, time controls
- `GameSession`: campaign state, checkpoint progress, player roster, config references
- `PlayerState`: inventory, status, choices, private information
- `PartyState`: shared supplies, wagon status, public progression
- `AIContentRequest` / `AIContentResponse`: bounded interfaces for generated content

## Roadmap Shape

1. Foundation and docs
2. Config-driven single-player prototype
3. Async multiplayer party flow
4. AI-assisted content generation with guardrails
5. Content tooling and validation
6. Encryption-ready networking model
7. Visual polish and campaign expansion

## Repo Documents

- [`README.md`](/Users/patrickteng/Projects/vibes-oregon-trail/README.md): project vision and constraints
- [`AGENTS.md`](/Users/patrickteng/Projects/vibes-oregon-trail/AGENTS.md): contributor and agent operating rules
- [`TODO.md`](/Users/patrickteng/Projects/vibes-oregon-trail/TODO.md): detailed backlog and open questions

## Current Status

This repository is currently in planning mode. The next step is to turn the product direction into:

- a concrete TODO list
- an agreed initial scope
- a first Expo/React Native project skeleton
