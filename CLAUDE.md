# CLAUDE.md

This file is loaded automatically by Claude Code at the start of every session.

## What This Project Is

A configurable multiplayer journey game — Oregon Trail-inspired — built with TypeScript, Expo, and React Native. The engine is designed to support multiple campaigns, not just Oregon Trail.

## Imported Context

@README.md
@AGENTS.md
@TODO.md
@docs/design-system.md

## Hard Rules

- TypeScript only.
- Config-driven content — no hardcoded landmark sequences, events, or story logic in app code.
- The game must remain fully playable with no network and no AI.
- Portrait-only orientation.
- All colors must come from the 32-color master palette in `docs/design-system.md`.
- Asset paths and naming conventions follow `docs/design-system.md` exactly.
- Do not introduce new dependencies without a clear reason.

## Current Status

Planning phase. No app code exists yet. The next step is initializing the Expo project and building the simulation layer per `TODO.md`.
