# TODO

## Immediate Vertical Slice

This is the build-first scope. If a task does not help deliver this slice, defer it.

### Goal

- [ ] Ship a single-device prototype where one player guides a shared wagon party through a short journey, makes repeated checkpoint decisions, and can win or lose in one sitting.

### Player-facing scope

- [ ] Start a new run from a config-defined scenario.
- [ ] View route progress, current checkpoint, supplies, party condition, and time.
- [ ] Travel through 6 to 8 landmarks/checkpoints.
- [ ] Choose from a small action set at checkpoints: travel, rest, forage, and shop when available.
- [ ] Resolve deterministic events that change resources, time, or status.
- [ ] Reach a final destination or fail from resource collapse, animal collapse, or party collapse.

### Must-build systems

- [ ] Initialize the Expo app with TypeScript and a simple navigation shell.
- [ ] Create a framework-agnostic TypeScript simulation layer.
- [ ] Define typed `ScenarioPack`, `RulePack`, `GameSession`, `PlayerState`, and `PartyState`.
- [ ] Load one starter scenario and one starter rule pack from config.
- [ ] Add config validation for landmarks, routes, stores, events, and endings.
- [ ] Add seeded deterministic selection for events and store stock.
- [ ] Implement checkpoint progression and route traversal.
- [ ] Implement core resources: food, money, wagon durability, and animal health.
- [ ] Implement time progression plus one simple time acceleration control.
- [ ] Implement one deterministic store flow and at least three deterministic event patterns.
- [ ] Implement local save/load for a single in-progress run.
- [ ] Build simple retro-styled placeholder UI for map, checkpoint, store, event, and run summary screens.

### Acceptance criteria

- [ ] A new run can be created entirely from config with no hardcoded landmark sequence in app code.
- [ ] One short Oregon Trail-inspired scenario is playable end to end in roughly 20 to 30 minutes.
- [ ] The same seed produces the same non-AI outcomes.
- [ ] At least one route fork creates a meaningful risk/reward difference.
- [ ] The player can buy supplies, hit events, recover or deteriorate, and either win or lose.
- [ ] The prototype remains fully playable with no network and no AI service.
- [ ] The data model still leaves room for 1 to 5 players later.

### Explicit defers until the slice is fun

- Live or networked multiplayer
- Runtime AI calls
- Signal or E2EE implementation
- Settlement, ranch, or descendant systems
- Production art/audio
- Multiple campaign themes

## Defaults For The Vertical Slice

- [x] One local player controls the party for the first playable build.
- [x] Party inventory is shared.
- [x] There are no asymmetric player roles in the first playable build.
- [x] There are no private choices or hidden-information systems yet.
- [x] Config packs are authored as TypeScript objects first.
- [x] AI interfaces may be scaffolded, but runtime AI stays off until after the slice works.
- [x] Save data is local-only for the first playable build.
- [x] Placeholder art and audio are acceptable until the loop is fun.
- [x] The starter campaign is short and ends after one complete route.

## Locked Product Direction

- [x] Tech stack is TypeScript + Expo + React Native.
- [x] First gameplay focus is the journey/travel loop.
- [x] Multiplayer target is 1 to 5 players.
- [x] First multiplayer shape after the slice is async/shared-phase play.
- [x] AI starts as a bounded content/runtime GM, not unrestricted control.
- [x] The design should leave a path toward stronger AI systems later.
- [x] The design should leave a path toward live multiplayer later.
- [x] Signal integration is not a first implementation milestone.
- [x] Descendants/ranch/family simulation is a future pillar, not v1 core scope.
- [x] Visual target is a 16-bit-inspired 80s/90s presentation.
- [x] Configurability should apply to both content and rules.

## Next Major Tracks After The Vertical Slice

- [ ] Async multiplayer foundations for 1 to 5 players.
- [ ] Bounded AI-assisted runtime content with deterministic fallbacks.
- [ ] Better content tooling and authoring workflows.
- [ ] Encryption-ready networking and state boundaries.
- [ ] Broader campaigns, visual polish, and larger content packs.

## Gameplay Systems

### Travel and pacing

- [ ] Define travel speed modifiers.
- [ ] Define the relationship between time, distance, weather, and risk.
- [ ] Decide how often checkpoints appear.
- [ ] Decide whether checkpoints are fixed nodes, dynamic nodes, or both.
- [ ] Decide whether route branches are visible in advance.
- [ ] Implement a simple pacing model before adding lots of edge cases.

### Supplies and economy

- [ ] Define the core item taxonomy.
- [ ] Define the first-pass economy and pricing model.
- [ ] Decide whether stores have regional inventories.
- [x] Keep stores deterministic in the vertical slice; revisit random and AI-driven variants later.
- [x] Keep resources party-shared in the vertical slice; revisit mixed ownership later.

### Survival and status

- [ ] Define hunger, injury, disease, morale, and fatigue scope for v1.
- [ ] Decide whether animal care is its own system or part of general travel durability.
- [ ] Keep oxen/animal care lightweight at first; do not build a separate pet sim unless it proves necessary.
- [ ] Define what can permanently end a run vs cause setbacks.

### Choice structure

- [ ] Define the checkpoint decision menu.
- [ ] Define event decision patterns.
- [ ] Define store interactions.
- [x] Defer private choices until after multiplayer implementation begins.
- [ ] Define branching endings.

## Multiplayer Design Details

- [x] Defer asymmetric player responsibilities until after the local slice is fun.
- [ ] Decide whether a leader/captain role exists.
- [ ] Decide how disputes or tie votes are resolved.
- [ ] Decide whether some events target one player privately.
- [ ] Decide whether inventory is mostly shared or mixed shared/private.
- [ ] Decide how to present "waiting for other players" without killing momentum.
- [ ] Define whether players can inspect history/logs of prior decisions.

## Security And E2EE Readiness

- [ ] Separate private player data from party-visible state in the data model.
- [ ] Decide which classes of data should be encryptable later.
- [ ] Define trust boundaries for client, transport, and any future backend.
- [ ] Research whether encrypted message payloads or encrypted save blobs are the first likely use case.
- [ ] Document why Signal is deferred from v1.
- [ ] Keep future protocol integration behind a transport abstraction.
- [ ] Avoid assuming the server can read all game state.

## Signal / Secure Messaging Research

- [ ] Research whether Signal protocol is a realistic fit for turn-based mobile game state sync.
- [ ] Compare Signal-based messaging with simpler application-layer encryption.
- [ ] Identify where Signal would help and where it would complicate multiplayer UX.
- [ ] Decide whether secure chat, secure choices, or secure save sync is the actual problem to solve.
- [ ] Revisit only after the base multiplayer model exists.

## Campaign And Landmark Backlog

- [ ] Define a starter Oregon Trail-inspired campaign with configurable landmarks.
- [ ] Keep landmark data separate from engine logic.
- [ ] Identify which landmarks are mandatory, optional, alternate-route, or scenario-specific.
- [ ] Add at least one non-historical "test campaign" to prove the engine is generic.

### Seed landmark ideas for the starter campaign

- [ ] Independence
- [ ] Kansas River crossing
- [ ] Fort Kearny
- [ ] Chimney Rock
- [ ] Fort Laramie
- [ ] Independence Rock
- [ ] South Pass
- [ ] Fort Bridger
- [ ] Soda Springs
- [ ] Fort Hall
- [ ] Snake River
- [ ] Fort Boise
- [ ] Blue Mountains
- [ ] The Dalles
- [ ] Willamette Valley

### Landmark system requirements

- [ ] Support mandatory checkpoints.
- [ ] Support optional detours.
- [ ] Support route forks with tradeoffs.
- [ ] Support store/rest/service landmarks.
- [ ] Support landmarks that unlock only under conditions.
- [ ] Support landmark-local event tables.

## Alternate Campaign Potential

- [ ] Prove the engine can support more than one setting.
- [ ] Define what would need to change to reskin the game into another campaign.
- [ ] Identify which systems are universally useful versus Oregon-specific.
- [ ] Keep notes on adjacent campaign ideas without letting them hijack v1.
- [ ] Treat ideas like naval campaigns, military logistics, sci-fi caravans, or other route-based adventures as future content-pack tests rather than immediate scope.

## Settlement / Descendant / Omni-Game Future Pillar

- [ ] Capture a future concept for players who stop and build instead of finishing the route.
- [ ] Capture a future concept for descendants continuing a family journey later.
- [ ] Capture what save data would need to persist across generations.
- [ ] Identify which current systems should avoid blocking these future directions.
- [ ] Keep this in roadmap notes until the base journey game is fun.

## Art And Audio

- [ ] Establish a visual reference board for 80s/90s-inspired presentation.
- [ ] Define the pixel-art level of detail for characters, wagons, landmarks, UI icons, and maps.
- [ ] Decide whether the map is top-down, side-view, node-based, or hybrid.
- [ ] Define animation needs for travel, weather, illness, damage, and arrival.
- [ ] Define a UI style guide for panels, buttons, borders, typography, and palettes.
- [ ] Decide whether to use handcrafted sprites, procedural variations, or both.
- [ ] Define an audio direction: sparse retro, synth-forward, ambient frontier, or hybrid.

## Assets

- [ ] Party/wagon sprites
- [ ] Oxen or travel-animal sprites
- [ ] Landmark illustrations
- [ ] Route map art
- [ ] Inventory icons
- [ ] Resource/status icons
- [ ] Event card backgrounds
- [ ] Store scene art
- [ ] UI chrome and panel frames
- [ ] Weather effects
- [ ] Sound effects for travel, shopping, mishaps, and milestone arrival
- [ ] Music loops for map, camp, danger, and victory/failure

## UX / Interface

- [ ] Define the main navigation flow.
- [ ] Define the structure of the journey HUD.
- [ ] Define the checkpoint screen.
- [ ] Define the store screen.
- [ ] Define the event resolution screen.
- [ ] Define the party status view.
- [ ] Define the route/landmark map view.
- [ ] Define the multiplayer session lobby.
- [ ] Define the history/logbook screen.
- [ ] Make sure the UI works on phones first.

## Data And Save Strategy

- [ ] Define local save requirements.
- [ ] Define save recovery requirements.
- [ ] Decide whether runs are resumable indefinitely.
- [ ] Decide whether sessions are authoritative on device, server, or hybrid.
- [ ] Define how config versions affect saved games.
- [ ] Define migration strategy for old saves when rules change.

## Technical Architecture

- [ ] Decide whether the core simulation engine should be framework-agnostic TypeScript.
- [ ] Keep React Native UI separate from simulation state transitions where possible.
- [ ] Define module boundaries for:
  - [ ] simulation
  - [ ] config loading
  - [ ] validation
  - [ ] multiplayer/session orchestration
  - [ ] AI integration
  - [ ] persistence
- [ ] Decide what must run offline.
- [ ] Decide what requires backend services.

## Backend / Service Questions

- [x] No backend is required for the local vertical slice.
- [ ] Decide whether async multiplayer needs a backend when that phase starts.
- [ ] If yes, define the smallest possible backend responsibility set.
- [ ] Decide how sessions are discovered or invited.
- [ ] Decide how AI requests are mediated securely.
- [ ] Decide how secrets are kept out of the client.

## Testing

- [ ] Add unit tests for state transitions and resource rules.
- [ ] Add tests for config validation.
- [ ] Add tests for route progression and checkpoint branching.
- [ ] Add tests for deterministic seeded outcomes.
- [ ] Add tests that the game remains playable with AI disabled.
- [ ] Add multiplayer tests for 1-player through 5-player sessions.
- [ ] Add tests for drop/rejoin and delayed decision submission.
- [ ] Add tests for save/load across versioned configs.

## Documentation

- [ ] Keep `README.md` aligned with current product direction.
- [ ] Keep `AGENTS.md` aligned with contributor expectations.
- [ ] Keep `TODO.md` as the source of truth for roadmap status.
- [ ] Add architecture notes once the project skeleton exists.
- [ ] Add a content pack authoring guide once the config format is chosen.

## Questions To Revisit After The Vertical Slice

- [ ] When should players gain asymmetric roles or private information?
- [ ] When should async multiplayer move from planned architecture to implementation?
- [ ] When should AI graduate from bounded content variation to stronger systems direction?
- [ ] Which alternate campaign should prove the engine is genuinely reusable?
- [ ] What is the smallest worthwhile secure-by-design step before actual E2EE work begins?
- [ ] Which part of the "omni-game" vision becomes a real roadmap item after the base journey loop is fun?
