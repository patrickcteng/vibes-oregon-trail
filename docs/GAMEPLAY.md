# Gameplay — vibes-oregon-trail

A design doc for the moment-to-moment experience of the first playable campaign. Vivid enough to imagine the game in your head; concrete enough to argue with; structured so the same engine bones can later host very different campaigns. The first stress tests are Carrier Command (real-time strategy + tactical) and a D&D-style campaign with an LLM dungeon master.

This is not a spec. Numbers presented as `TUNING` are placeholders that get filled in during the simulation-layer build with a balance sweep. Section 17 also preserves explicit open questions. Everything else is a real design decision.

Reads top-to-bottom in about twenty minutes.

---

## 1. The pitch

You are leading a small wagon party out of Independence, Missouri in the spring of 1848. You have a wagon, a team of oxen, four other settlers, and enough supplies to last maybe two weeks if nothing goes wrong. The Willamette Valley is two thousand miles away. Things will go wrong.

The game is a pixel-art, portrait-orientation, single-device journey through a configurable route of landmarks and decisions. You travel a day at a time, watching your supplies tick down. You stop at forts to trade. You ford rivers and sometimes lose what you're carrying. You hunt — and *hunting* is its own little aim-and-shoot mini-game, not a coin flip. You rest when morale runs low. You take the shortcut and pay for it, or you take the long way and pay for it differently.

It is not Oregon Trail 1985. It is what Oregon Trail 1985 *felt* like — the dread, the small triumphs, the texture of frontier scarcity — translated into a phone game a person born in 2010 would actually enjoy holding for twenty-five minutes. Modern game design says you can lose a run, but you should not lose a run to a single coin flip three minutes in. Modern mobile UX says swipes and haptics and autosave. Modern tech says cloud sync and shareable run summaries. The pixels stay 16-bit. Everything around them is 2026.

---

## 2. A typical session, narrated

Imagine sitting on a couch on a Tuesday evening. You have twenty-five minutes before something else.

You open the app. The title screen is a wagon silhouette against a warm sunset (`screen_title.png`). You tap *Continue Run*. The autosave from last night drops you back at Fort Kearny, day 28 of the campaign. The HUD across the bottom shows food at 41%, water at 70%, wagon condition at 88%, party morale at "Steady."

You're at a checkpoint, so the screen is the Fort Kearny landmark scene (`landmark_fort_kearny.png`) with a panel of actions tucked over the lower third: **Travel**, **Rest**, **Forage**, **Hunt**, **Shop**. You tap *Shop*. The store screen slides in (`store_background.png`) with the shopkeeper sprite behind the counter. Food is overpriced this far out. You buy a single sack of flour and 20 rounds of ammunition. The money bar drops from `$340` to `$280`. You tap *Leave*.

Back at the checkpoint. You tap *Hunt*. The screen transitions into a different mode entirely — a side-on plains scene, your settler with a rifle on the left, a small herd of bison moving right to left in the middle distance. The route loop has paused; you're in a sub-simulation now. Drag to aim, tap to fire. You spend 8 rounds, drop two animals, and the sub-sim ends with a result card: `+92 lbs food, −8 ammunition`. You tap to dismiss. You're back at the checkpoint, food bar nudged up.

You tap *Travel*. The map view comes up (`map_background.png`) with your current node glowing gold and the route ahead dotted toward Chimney Rock. You swipe right to advance days. Each swipe is one in-game day. The day counter ticks. Food drops a notch every swipe. A small haptic fires on day 31. On day 33, an event interrupts the swipe.

Event card: `event_storm.png`. The text reads, *"A late-spring storm catches you in the open. The wagon canvas is taking on water. Press on, or make camp?"* Two buttons. *Press on* — `−1 day, −5% wagon condition, +chance of illness`. *Make camp* — `−2 days, −food, +morale`. The costs are previewed. The dice are not.

You press on. The screen flashes. The wagon condition bar drops 7% (worse than the preview said it might be — modern design says costs are honest in expectation, not in worst case). Nobody gets sick this time. You exhale.

Day 38: Chimney Rock (`landmark_chimney_rock.png`). The spire fills the upper two thirds of the scene. Action menu again. You *Rest* for two days. Morale ticks up. Food ticks down. Your sick party member ("Hannah, ill") moves from `status_sick.png` back to `status_healthy.png`.

Day 40: a fork in the route. The map zooms in. *Continue along the Fort Bridger detour (longer, safer, restock)* or *Take the Sublette Cutoff (shorter, drier)*. The tradeoffs are listed before you commit. You take the Fort Bridger detour because your wagon is bruised and the chance to restock is worth the extra days. You spend the next twelve days watching food slide down, but the water bar never gets scary.

Day 52: Fort Bridger. You restock. You sell the spare wagon parts you've been carrying. You feel okay about your run for the first time.

The session ends here. You tap the home button. The game autosaved at Fort Bridger. The next time you open it, you'll be at exactly day 52, same supplies, same party, same momentum. Total time elapsed: twenty-three minutes.

You did not win. You did not lose. You made progress and made decisions and the run is still alive. That's the unit of play.

---

## 3. The core loop

The minute-to-minute structure underneath the narrative above:

```
  ┌──────────────────────────────────────────────────────┐
  │                                                      ↓
  │   ┌─────────┐    ┌────────────┐    ┌─────────────────────┐
  │   │ TRAVEL  │ ─→ │ CHECKPOINT │ ─→ │ DECISION            │
  │   │ (days)  │    │ (landmark) │    │ (action menu OR     │
  │   └─────────┘    └────────────┘    │  fork choice)       │
  │       ↑                            └──────────┬──────────┘
  │       │                                       ↓
  │       │                            ┌─────────────────────┐
  │       │                            │ RESOLUTION:         │
  │       │                            │  • event card       │
  │       │                            │  • state mutation   │
  │       │                            │  • drop into        │
  │       │                            │    SUB-SIMULATION   │
  │       │                            │    (hunt, combat,   │
  │       │                            │    crossing, …)     │
  │       │                            └──────────┬──────────┘
  │       │                                       ↓
  │       │                            ┌─────────────────────┐
  │       └────────────────────────────│ CONSEQUENCES        │
  │                                    │ (state delta        │
  │                                    │  applied, autosave) │
  │                                    └─────────────────────┘
```

Travel ticks consume days and resources. Checkpoints are nodes that interrupt travel and surface a decision. Decisions resolve in one of three ways: an event card with previewed choices, a direct state mutation (Rest 2 days), or a hand-off into a *sub-simulation* — a self-contained gameplay mode with its own controls and screens. The sub-sim runs to a conclusion and returns a typed state delta. Consequences are applied, the player returns to the loop.

**Engine callout.** `GameSession` runs this loop. The current position is a `NodeGraph` cursor. Each `Node` exposes an `Action` set, sourced from a `Director` (Section 15). Choosing an `Action` produces either an `Encounter` (resolved in-place) or launches a `Simulation` (Section 9). Both return a state delta applied to `PartyState`, `PlayerState`, `Vessel`, `Crew`, and `Resource` containers. The next loop iteration begins.

The loop is identical across campaigns. The cursor moves through an `archipelago` instead of a `trail`. The action set at an island is `capture` / `refuel` / `produce` / `defend` instead of `travel` / `rest` / `forage` / `shop`. The sub-sim that fires from a Combat action is a real-time tactical instead of a hunting mini-game. The wiring is the same.

---

## 4. The vessel

The wagon is the mobile home base. It carries everything: the crew, the supplies, the spare parts, the ammunition, the money. Its condition is a single percentage from 0 to 100. Rivers, storms, and rough terrain chip away at it. Spare wagon parts repair it at any checkpoint.

Visual: `wagon_idle.png` when parked, the four-frame `wagon_travel_*` cycle while traveling, `wagon_damaged.png` below 30% condition, `wagon_destroyed.png` at 0%.

The wagon does not move on its own. It needs the oxen team. If the oxen die or are sold, the wagon stops. (Whether oxen are modeled as a `Resource` quantity or a small `Crew` of two animals is an open question — see Section 17.)

A run ends if the wagon hits 0% condition with no spare parts AND no money AND no nearby store. This is rare. Most runs end from a slower spiral, not a single catastrophic event. See Section 11.

**Engine callout.** `Vessel` is the player's mobile state container. It has a condition meter, an inventory (typed by `Resource`), a position on the `NodeGraph`, and a dependency on a propulsion entity (oxen for OT; engines and fuel for CC; nothing for D&D — the "vessel" is abstract). The rule pack defines what damages it, what repairs it, and what immobilizes it.

---

## 5. The crew

A party of one to five settlers. The first playable campaign ships with a fixed party of five — you, three named companions, and one named child. (Names and portraits come from the scenario pack, not the engine.)

Each crew member has:

- **Health** — `healthy`, `injured`, `sick`, `exhausted`, `dead`. Drawn from the `status_*.png` icons.
- **Morale** — `high`, `steady`, `low`, `critical`. The party shares a single morale value in the slice; per-person morale is a future extension.
- **Status effects** — temporary modifiers from events (a sprained ankle slows travel for three days; a bout of dysentery doubles food consumption for a week).

Crew are mostly interchangeable in the slice. They don't have stats or special skills yet. The data model leaves room for `role` and `skills` fields so a later campaign can have a doctor who heals faster, a hunter who returns more meat, or a D&D wizard with spell slots.

A crew member dying is a setback, not an ending. The run ends only if the *entire* party dies. Modern design: losing a kid in 1848 was horrific and the game does not pretend otherwise, but it does not punish the player by deleting their save.

**Engine callout.** `Crew` is a roster of `Agent` entities. Each `Agent` has health state, morale contribution, optional role/skills, status effects, and a private data slot (a future affordance for asymmetric multiplayer). The rule pack defines what changes their state. In Carrier Command, `Crew` is squadron pilots and ship officers. In D&D, `Crew` is the player characters with classes, levels, HP, and spell slots.

---

## 6. Resources & economy

The resources the engine tracks for the first playable campaign:

| Resource       | Icon                       | Depletes from        | Restores from              |
|----------------|----------------------------|----------------------|----------------------------|
| Food           | `icon_food.png`            | Every travel day     | Forage, hunt, shop         |
| Water          | `icon_water.png`           | Every travel day     | Crossings, springs, shop   |
| Money          | `icon_money.png`           | Shopping             | Selling spare goods        |
| Ammunition     | `icon_ammunition.png`      | Hunting sub-sim      | Shop, find-supplies events |
| Medicine       | `icon_medicine.png`        | Treating illness     | Shop, find-supplies events |
| Wagon parts    | `icon_wagon_parts.png`     | Repairs              | Shop, scavenge events      |
| Clothing       | `icon_clothing.png`        | Cold weather, wear   | Shop                       |
| Tools          | `icon_tools.png`           | Repairs, foraging    | Shop                       |
| Oxen           | `icon_oxen.png`            | Death, sale          | Shop (rare)                |

Burn rates and prices are `TUNING`. The principle: food and water are the heartbeat (always burning), money and ammunition are the gear (spend at decision points and in sub-sims), wagon parts and medicine are the safety net (you don't need them until you really need them).

Resources interact. A few examples (illustrative, not exhaustive):

- **Low water + crossing a desert stretch** raises illness chance for the next `TUNING` days.
- **Low food + low morale** compounds — hungry parties argue, argument-events become more likely.
- **Cold weather + no clothing** drives a "frostbite" status that costs travel days.
- **Wagon condition below 30%** drops travel speed by a `TUNING` percentage. Going below 10% adds a chance of a "breakdown" event each travel day.

The economy is deliberately scarce but not punishing. A player who reads their HUD and stops at every fort can finish the run. A player who never stops at forts probably cannot. There is no single resource whose collapse instantly ends the run; collapse is always a cascade.

**Engine callout.** `Resource` is a typed quantified item with an id, a current amount, optional max, and a unit. The rule pack defines `burnRates` (per travel day, per event type) and `interactions` (predicates on resource states that gate or modify events). Carrier Command swaps in `fuel`, `ammo`, `manufacturing capacity`, `island control points`. D&D swaps in `HP per character`, `spell slots`, `gold`, `rations`. The container is the same.

---

## 7. The route

The first playable campaign uses **eight landmarks** from Independence to Willamette Valley, with **one fork**.

Linear order with the fork in the middle:

```
  Independence (start, town)
        │
        ↓
  Kansas River Crossing (crossing)
        │
        ↓
  Fort Kearny (fort)
        │
        ↓
  Chimney Rock (landmark)
        │
        ↓
  Fort Laramie (fort)
        │
        ↓
       ╔═══════════════════════════╗
       ║ FORK                      ║
       ║                           ║
       ║  Sublette Cutoff          ║
       ║  (shorter, drier, riskier)║
       ║         OR                ║
       ║  Fort Bridger detour      ║
       ║  (longer, safer, restock) ║
       ╚═════════════╤═════════════╝
                     │
                     ↓
          South Pass (mountain)
                     │
                     ↓
            Snake River (crossing)
                     │
                     ↓
          Willamette Valley (end, victory)
```

Each node has a `type` that controls which actions are available there:

| Node type     | Actions available                                             |
|---------------|---------------------------------------------------------------|
| `town`        | Travel, Rest, Forage, Shop (large inventory), Save            |
| `fort`        | Travel, Rest, Forage, Hunt, Shop (modest inventory)           |
| `crossing`    | Ford / Caulk / Pay-toll (if available), Forage, then Travel   |
| `landmark`    | Travel, Rest, Forage, Look (flavor text + small morale boost) |
| `mountain`    | Travel (slower), Rest, Forage, Hunt                           |

The Fort Bridger detour is conditional: if the player chose the Sublette Cutoff at the fork, they skip Fort Bridger entirely. This is the single piece of state-dependent route shape in the slice.

The map (`map_background.png`) shows the full route as a dotted parchment line from lower-right to upper-left. Visited nodes use `node_visited.png`, the current node uses `node_current.png`, unvisited nodes use `node_unvisited.png` or their type-specific variant (`node_fort.png`, `node_crossing.png`, `node_mountain.png`, `node_town.png`). The fork's two branches are both drawn lightly until the player commits.

**Engine callout.** `NodeGraph` is a graph of `Node`s. Each `Node` carries its type, its `Action` set, its `Encounter` table, its presentation metadata (which `landmark_*.png` to render), and any conditional traversal predicates. OT's graph is directed and mostly linear. Carrier Command's is undirected and densely connected. D&D's is *generated on demand* by an LLM `Director` (Section 15) as the player explores — same `NodeGraph` data structure, different content source.

---

## 8. Decision shape

Three decision archetypes cover every player choice in the slice.

### 8.1 Checkpoint menu

At a node, the action panel presents two to five buttons. Always tap-once-to-commit. Always cancellable until commit. Each button has:

- A label (`Travel`, `Rest`, `Forage`, `Hunt`, `Shop`)
- An icon (`icon_*.png`)
- A short preview of cost in days and resources (`Rest 1 day · +morale · −food`)
- A disabled state with reason if unavailable (`Shop — no money`)

Modern UX: previews are always honest about the *expected* cost. Stochastic outcomes (Hunt returns 0–80 lbs of meat depending on player skill in the sub-sim) are previewed as a range, not a hidden roll.

### 8.2 Event resolution

When an `Encounter` fires mid-travel, the screen transitions to an event card (`event_*.png`) with a title, two to three sentences of text, and two or three response buttons. Each button shows its previewed cost and a hint at its risk profile (`Press on · −1 day · risk of illness`).

Outcomes are deterministic against the seed for static content. The same seed + same decision = the same outcome. (Tap-replay of a bad run produces the same dice rolls — this is intentional for testing and for replays.) Skill-based sub-sims add their result or input log to the replay record; LLM-generated content is recorded in the autosave so replays remain reproducible — see Section 15.

The text body comes from the `Director`. A static director reads pre-authored copy; an LLM director generates variants in real time.

### 8.3 Fork decision

At a fork node, the map zooms in to show the two branches as a comparison panel side by side. Each branch shows:

- Estimated days
- Risk descriptors (`drier`, `safer`, `mountain pass`)
- Available restocks along the way
- An illustrative single-line summary

The player commits with one tap. The branch they took is highlighted gold on the route map for the rest of the run. The branch they skipped fades.

This is the *modern game design* part: tradeoffs are visible before commit. There is no "hidden right answer" the player has to guess. The choice is interesting because both branches are viable in different states, not because one is obviously better and the player didn't know.

**Engine callout.** Every decision is an `Action` invocation. `Action`s have a label, an icon, an availability predicate, a previewed cost, and a resolver. The resolver returns either an `Encounter` (resolved in-place) or a `Simulation` launch (Section 9). Rule packs define availability and outcome distributions; `Director`s define labels and copy.

---

## 9. Sub-simulations

The strategic loop is most of the game. But some decisions deserve to be more than a button tap and a state delta. *Hunting* in Oregon Trail. *Flying a Manta* in Carrier Command. *A turn-based combat encounter* in a D&D session. These are **sub-simulations**: self-contained gameplay modes with their own controls, screens, and rules that drop in from the strategic loop, run to a conclusion, and return a typed state delta.

The pattern is the same in every campaign:

1. A decision in the strategic loop launches a sub-simulation.
2. The strategic loop suspends. The sub-sim takes over the screen and input.
3. The player plays the sub-sim to its conclusion (or quits — quitting still returns a result, just an "aborted" one).
4. The sub-sim returns a typed result.
5. The result is folded back into strategic state. Strategic loop resumes. Autosave fires.

### 9.1 Examples per campaign

**Oregon Trail (slice + near-future):**

- *Hunting* — short aim-and-shoot mini-game when the player chooses Hunt at a node. Side-on view, animals moving across the middle distance, rifle on the left. Drag to aim, tap to fire, limited by ammunition available. Returns meat (food resource), spent ammunition, and a small accident risk. Sub-sim duration: 30–60 seconds.
- *River crossing* — a planning mini-game: pick a ford point on a small cross-section diagram, set ox speed, decide whether to lighten the load. Returns wagon damage, lost cargo, and days spent. Replaces the simple Ford/Caulk action when scope allows.
- *Store* — already a sub-screen in the slice. Technically the simplest sub-sim: the loop pauses, the store screen takes inputs, the cart is committed, the player returns. Worth treating as a sub-sim so the engine pattern is consistent everywhere.

**Carrier Command (future):**

- *Combat engagement* — real-time tactical mode. Top-down map of the engagement zone. Walruses on islands, Mantas in air, ship-to-ship gunnery. Player can control individual units or assign orders. Pause-and-plan supported. Returns damage taken and dealt, unit losses, fuel/ammo spent, island control changes. Sub-sim duration: minutes.
- *Production order* — a focused interface for an island's production capacity. Pick what to build, accept time and material cost. Returns the queued build order.
- *Strategic engagement of the enemy carrier* — the campaign-final boss fight. Full bespoke mode, longer than a normal engagement, with its own state and rules.

**D&D campaign (future):**

- *Combat encounter* — grid-based or theater-of-the-mind tactical combat against monsters surfaced by the DM. Initiative order, actions per turn, dice rolled visibly. Returns HP changes, items gained, XP, narrative consequences.
- *Skill challenge* — a short sequence of dice rolls under DM narration. Returns a success/failure ladder result.
- *Roleplay scene* — text-driven exchanges with NPCs. May or may not need its own sub-sim wrapper — short scenes can stay in the event-card UI; long scenes promote to their own mode.

### 9.2 The contract

Every sub-sim takes a typed input: an immutable strategic-state snapshot plus the specific capabilities it is allowed to use. A hunt gets ammunition available, terrain, party modifiers, and allowed result types. It does not get a mutable `GameSession`. A CC combat engagement gets the participating units, local map, fuel/ammo caps, and allowed control-point outcomes. A D&D combat encounter gets the combatants, initiative rules, and allowed reward/damage bounds.

The sub-sim owns temporary internal state while it is active. On completion, abort, or interruption recovery, it returns a typed `SimResult` with four things: `status` (`completed` or `aborted`), a strategic state delta, an event log for the run history, and replay metadata. The replay metadata can be a compact input log, a final result snapshot, or both, depending on the sub-sim.

This boundary is what keeps the engine sane: campaigns can ship totally different sub-sim implementations — menu-based, real-time, dice-driven, physics-driven — without touching the strategic loop. The strategic loop just sees `launch(SimInput) → SimResult`. Strategic state is read-only while the sub-sim runs and mutates only when the `SimResult` is committed.

Sub-sims also have their own visual treatment. The hunting sub-sim uses a different scene composition than the route view. The CC combat sub-sim is a top-down tactical layer; the strategic CC view is a campaign map. The mode switch is signaled to the player with a deliberate transition (a fade, a curtain wipe) so the rules-shift is obvious.

Autosave records a `pendingSimulation` when the app backgrounds or is interrupted mid-sub-sim. For the OT slice, resuming mid-hunt restores the hunt if the renderer can safely reconstruct it; otherwise the hunt resolves as an aborted result with ammunition spent so far and no positive food reward. Longer future sub-sims, like CC combat, should treat `pendingSimulation` as required resumable state rather than a forfeit.

### 9.3 Why sub-sims matter for the engine

The original Carrier Command lens (Section 16) flagged tactical sub-screens as the *most likely* abstraction to break. Making sub-sims first-class de-risks that: every campaign exercises the same pattern. The OT slice ships at least one (hunting) to prove the pattern works before CC pushes it harder.

**Engine callout.** `Simulation` is a self-contained gameplay mode with its own update tick, render layer, and input handling. It exposes `start(input: SimInput): void` and `onComplete(callback: (result: SimResult) => void)`. The strategic loop wraps the launch in a "drop into sim" UI transition and a "return with delta" hand-off. Sub-sims can be menu-based (store), real-time (hunting, CC combat), or hybrid (D&D combat with initiative). The engine provides the lifecycle and the data contract; each `Simulation` implementation owns its own rules and rendering.

---

## 10. Time & pacing

One travel tick = one in-game day. A swipe on the travel screen advances one day. A long-press advances a "rest period" of two to three days at once (the user picks).

Target campaign length: **60 to 90 in-game days**, finishing in **~25 real minutes** of active play. The math: ~70 days at ~20 seconds of active decision-making per day = ~23 minutes. Idle travel days (where nothing happens) are compressed by the swipe-batch UX — three uneventful days flick by in a second.

The time model for the strategic loop is **strictly turn-based**. There is no real-time component, no cooldowns measured in wall-clock seconds, no "energy" mechanic that locks the player out for an hour. Sub-simulations may run real-time internally (CC combat) but the strategic clock pauses while a sub-sim is active.

**Engine callout.** `TimeModel` is a pluggable component on the rule pack. The OT strategic loop uses `TurnBased { unit: 'day', tick: 'manual' }`. Carrier Command's strategic loop could use `RealTimeTick { unit: 'second', rate: '1tick/100ms', pausable: true }`. D&D uses `TurnBased { unit: 'scene', tick: 'manual' }`. Each `Simulation` declares its own internal time model independently.

---

## 11. Failure model

What ends a run:

1. **Vessel destruction.** Wagon at 0% condition, no spare parts in inventory, no money in inventory, and not within one day's travel of a store. (Modern design: this is hard to actually achieve. The player has to ignore the condition meter for many days in a row.)
2. **Crew wipe.** Every party member dead.
3. **Resource collapse with no recovery path.** Food at 0, no ammunition for hunting, no money for shop, no friendly node within travel range. Again, hard to reach without compounding neglect.

What does *not* end a run:

- A single bad event roll.
- A single party member's death.
- Going broke at the wrong fort (you can still travel, hunt, forage).
- Wagon damage above 0%.
- A bad sub-sim outcome (you whiffed the hunt — you spent ammo for no food, but the run continues).

**Setbacks are recoverable.** The game punishes a *pattern* of neglect over a series of decisions, not a single dice roll. This is the central modern-design departure from 1985 Oregon Trail, which would happily end your run on day three because you contracted typhoid.

**Autosave** writes after every checkpoint (every decision commit, not every travel day, and after every sub-sim completes). If the app is interrupted mid-sub-sim, the save contains a `pendingSimulation` record so the game can resume or resolve the sub-sim consistently. A failure offers a one-tap *Restart from last checkpoint* option, which rolls back to the most recent committed autosave.

Replays use the same seed for deterministic content, recorded sub-sim replay metadata for skill-based modes, and recorded LLM responses for generated content (Section 15), so dice rolls, hunt outcomes, and event copy repeat.

This is balanced against "saves trivialize the game" by limiting the rollback to the *last* checkpoint (no save-scumming back five hours), and by keeping the campaign short enough that a full restart is also viable.

**Engine callout.** `Goal` is the rule pack's win/lose evaluator. It runs after every state mutation and returns one of `running`, `won`, `lost(reason)`. Rule packs swap it: OT's goal is `reach('willamette_valley') AND crew.aliveCount > 0`; Carrier Command's would be `controlledIslands >= N OR enemyCarrierDestroyed`; D&D's is DM-defined per campaign.

---

## 12. Modern mobile UX hooks

The 16-bit pixel art lives inside a modern phone shell. Specific patterns:

**Gestures:**
- Swipe right on travel screen = advance one day.
- Long-press travel button = batch-advance two to three days (player picks duration in a small popover).
- Pinch-out on map = zoom in. Two-finger drag = pan within the route.
- Swipe down on any modal = dismiss.
- Long-press on any resource bar = show detailed breakdown (current, max, burn rate, projected days-until-empty).

**Haptics:**
- Light tap on every button press.
- Medium tap on a resource crossing a 50% / 25% / 10% threshold (so the player feels their food dropping).
- Heavy tap on event reveal, on checkpoint arrival, and on sub-sim launch and exit.
- Failure haptic on run ending.

**Layout:**
- Portrait-locked (per `docs/design-system.md`).
- 16px minimum margin from screen edges for any tappable UI (per the safe-area rule in the design system).
- Tap targets minimum 32px tall (two tiles), even when the visual element is smaller — extend the hit region invisibly.
- Default to **dark mode** — the palette's `UI Dark` is already the panel background, so dark is the native presentation; a light-mode toggle uses `Parchment` for backgrounds instead.

**Modern tech features:**
- **Autosave** to local device after every checkpoint and every sub-sim completion.
- **Cloud sync** to iCloud (iOS) and Google Drive (Android), opt-in, off by default. Sync window: the most recent autosave per device.
- **Share-as-image**: at end of run, a one-tap action generates a PNG of the route map with the player's path drawn in, key stats overlaid (days survived, distance traveled, party at end), and a one-line ending caption. Designed for messaging apps and socials.
- **Optional LLM director**: per Section 15, a toggle in settings enables LLM-generated content variants. Off by default in the slice. The deterministic baked content is always the fallback.

None of these features ship for the slice except autosave and dark mode. They are listed here so the data model and UI patterns leave room for them.

---

## 13. Multiplayer stance

The first playable campaign is single-device and single-controller: one local player makes decisions for the whole wagon party. That keeps the slice focused on whether the journey loop is fun.

The engine still treats multiplayer as a first-class future shape. A `GameSession` has a `players` list from the start, even if the slice contains one local player. Shared campaign facts live in `PartyState`: route position, current node, wagon/vessel condition, shared inventory, party morale, public crew condition, event history, and committed decisions. Per-player facts live in `PlayerState`: identity, local preferences, private choices, future hidden information, and any data that may need encrypted transport later.

Async multiplayer later changes who is allowed to commit an `Action`, not what an `Action` is. A checkpoint decision can become a leader commit, a vote, or a proposal/confirm flow without rewriting the route loop. The important boundary is that `PartyState` is the public truth the group shares, while `PlayerState` is the private or player-owned layer the engine keeps separate.

**Engine callout.** `GameSession` owns `players`, `PartyState`, and a map of `PlayerState` records keyed by player id. The OT slice uses one local player and mostly empty private state. Future async play adds decision ownership and synchronization around the same state objects. Future encryption wraps transport/storage for selected `PlayerState` or message payloads without forcing `PartyState` and private data into one blob.

---

## 14. What the engine has to do

Pulling the inline engine callouts into one consolidated list. Each item is one line. Schemas come during the simulation-layer build, not in this doc.

- `ScenarioPack` — pre-authored content: `NodeGraph` shape, `Node` action sets, `Encounter` tables, endings, presentation metadata (which `landmark_*.png` per node, which `event_*.png` per encounter, copy strings).
- `RulePack` — pacing knobs, resource burn rates and interactions, economy (prices, store inventories), `TimeModel`, `Goal` evaluator, AI permissions and budgets.
- `GameSession` — current campaign state, players, RNG seed, checkpoint history, autosave snapshots, pending simulation state, recorded sub-sim replay metadata, and recorded LLM responses for replay.
- `PartyState` — public shared state: route position, current node, wagon/vessel condition, shared inventory, party morale, public crew condition, event history, and committed decisions.
- `PlayerState` — per-player state: identity, local preferences, private choices, future hidden information, and encryption-ready player-owned data.
- `Vessel` — mobile state container (roster of one for OT, can be many for CC) with condition meter, inventory, propulsion dependency, position on the `NodeGraph`.
- `Crew` — roster of `Agent`s with health, morale, status effects, optional role/skills, private data slot.
- `Resource` — typed quantified item with id, amount, optional max, unit.
- `Action` — labeled, icon'd, availability-predicated, cost-previewed, resolver-bearing decision primitive.
- `Encounter` — in-place resolver returning a state delta over `Vessel` / `Crew` / `Resource`.
- `Simulation` — self-contained sub-game with own update/render/input; lifecycle is `start(input) → onComplete(result)`. Section 9.
- `NodeGraph` and `Node` — graph structure of typed nodes with action sets and encounter tables.
- `TimeModel` — pluggable turn-based or real-time-tick component, declared per loop (strategic and per-Simulation).
- `Goal` — pluggable win/lose evaluator on the rule pack.
- `Director` — content source. Variants: `StaticDirector` (baked scenario pack), `LLMDirector` (LLM-driven), `HybridDirector` (composition). Section 15.

The engine is **framework-agnostic TypeScript**. None of it imports React Native. The UI layer (Section 12) consumes the engine through plain function calls and observable state. `Simulation` implementations may use React Native or a different renderer (Skia, etc.) per sub-sim's needs — the engine itself stays renderer-agnostic.

---

## 15. Content sources & directors

A scenario pack is a *content source*. The first playable campaign ships its content source as a static TypeScript object: every node, every event, every line of copy is authored ahead of time. This is the deterministic, AI-free fallback the project's pillars require.

The engine supports two other content shapes:

**LLM-directed content.** A D&D-style campaign where the dungeon master is an LLM. Instead of a baked `NodeGraph`, the content source generates nodes on demand as the player explores. The LLM has read access to the current `GameSession` state and write access to a constrained authoring API: "create the next node," "spawn an encounter at the current node," "produce dialogue for this NPC," "adjudicate a skill check." The output is validated against the same schemas a static scenario pack uses, so the engine cannot tell the difference. From the strategic loop's perspective, an LLM-generated node is identical to a pre-authored one.

**Hybrid content.** Pre-authored skeleton (the eight Oregon Trail landmarks stay fixed) with LLM-generated leaves (event flavor text, NPC dialogue, store gossip varies per playthrough). The toggle is per-content-type: a player can run the slice with deterministic events plus AI-generated NPC dialogue, or vice versa.

### 15.1 The Director interface

Every campaign provides a `Director` implementation:

- `StaticDirector` — reads everything from a baked `ScenarioPack`. Used by the OT slice.
- `LLMDirector` — calls an LLM to generate content on demand, validates output, falls back to a baked default on failure or when AI is disabled. Used by the D&D campaign and by the optional AI-flavor toggle in OT.
- `HybridDirector` — composes the two above. Used by any campaign that wants some pre-authored content and some generated.

The strategic loop only ever talks to its `Director`. It calls `director.nextNode()`, `director.eventFor(node)`, `director.dialogueFor(npc)`, `director.adjudicate(action, context)`. The `Director` decides whether to read from a pack, call an LLM, or compose both.

### 15.2 Safety, cost, latency

LLM content has three properties the engine has to manage explicitly:

- **Safety.** Generated content must validate against the campaign's schemas (a generated event must declare its outcome distribution; a generated NPC must declare their inventory and disposition; a generated combat encounter must obey the rule pack's level-appropriate difficulty band). Out-of-schema responses are rejected and the static fallback is used. The LLM never gets unmediated write access to game state.
- **Cost.** LLM calls cost money. The `Director` declares a per-decision budget and a per-session cap, both `TUNING`. When the budget is exhausted, the campaign degrades to its static fallback rather than failing.
- **Latency.** Generation can take seconds. The engine never blocks the player on a network call. Either content is generated speculatively in the background while the player is in the previous loop iteration, or the player sees a short "the DM is thinking..." interstitial with a guaranteed bounded wait (`TUNING`, probably 3–5 seconds max before falling back).

### 15.3 Determinism and replay

Static scenario packs are deterministic against the RNG seed (same seed + same decisions = same outcomes). LLM-generated content cannot be deterministic in the same way — the same prompt to the same model can return different text on a different day.

The engine handles this by **recording** generated content into the autosave snapshot. A replay of a saved run reuses the recorded content; a fresh run generates anew. Saves are self-contained: a saved D&D run can be reloaded six months later, on a different model version, and the world the player remembers is still the world they get back. This is how the engine keeps replays viable for testing and post-mortem without forcing the LLM to be reproducible.

**Engine callout.** `Director` is the content-source interface every campaign provides. Variants compose. The OT slice ships with `StaticDirector` only; the AI-flavor toggle later wraps it in a `HybridDirector { static: pack, llm: flavorDirector }`. A D&D campaign ships with `LLMDirector` for nodes and dialogue, `StaticDirector` for core combat rules and creature stat blocks. Carrier Command would likely use `StaticDirector` for v1 with a future option to LLM-generate enemy tactics or procedural island layouts.

---

## 16. Campaign lenses: Carrier Command and D&D

The whole point of the abstraction set above is to prove, on paper, that the same engine can host very different campaigns. Side-by-side mapping for the three most distant cases:

| Abstraction       | Oregon Trail (slice)                              | Carrier Command (future)                              | D&D (future)                                          |
|-------------------|---------------------------------------------------|-------------------------------------------------------|-------------------------------------------------------|
| `Vessel`          | Wagon (one)                                       | Aircraft carrier (one, later many)                    | Adventuring party as an abstract "we" (one)           |
| `Crew`            | Five settlers with health/morale                  | Squadron pilots, ship officers, deck crew             | Player characters with classes, levels, HP, slots     |
| `PartyState`      | Shared wagon state, route, supplies, event log    | Shared carrier task force state and island campaign   | Shared party state, quest log, visible world state    |
| `PlayerState`     | One local player now; private slots reserved      | Officer/pilot assignments and private preferences     | Individual PC ownership, private notes, hidden info   |
| `NodeGraph`       | Directed, linear with one fork (pre-authored)     | Undirected archipelago (pre-authored)                 | Generated on demand by `LLMDirector`                  |
| `Node` types      | town, fort, crossing, landmark, mountain          | island_friendly, island_neutral, island_hostile       | room, corridor, shrine, lair, town, wilderness        |
| `Action`s at node | Travel, Rest, Forage, Hunt, Shop                  | Deploy Walrus, deploy Manta, capture, refuel, defend  | Search, parley, attack, cast, retreat, rest           |
| `Resource`        | Food, water, money, ammo, parts, oxen             | Fuel, ammo, manufacturing, control points             | HP/character, spell slots, gold, rations, inspiration |
| `Encounter`       | Storm, illness, broken wheel, theft               | Enemy fleet contact, weather, defection               | Monster, trap, NPC dialogue, divine omen              |
| `Simulation`      | Hunting, river crossing, store                    | Combat (real-time tactical), production order         | Combat (grid tactical), skill challenge, social scene |
| `Director`        | `StaticDirector` (baked pack)                     | `StaticDirector` mostly; later procedural islands     | `LLMDirector` (the DM is the LLM)                     |
| `TimeModel` (strategic) | Turn-based, one tick per day                | Real-time tick with pause                             | Turn-based scene-by-scene                             |
| `TimeModel` (sub-sim)   | Hunting: real-time short. Store: turn-based | Combat: real-time with pause                          | Combat: turn-based initiative                         |
| `Goal`            | Reach Willamette Valley alive                     | Control N islands by turn T, OR destroy enemy carrier | DM-defined per campaign (quest, level, story beat)    |
| Failure           | Vessel/crew/resource collapse                     | Carrier sunk OR no islands controlled OR enemy wins   | Party wipe OR DM-declared ending                      |

### 16.1 Where it gets interesting

- **Real-time vs turn-based.** OT's swipe-per-day pacing is a thin wrapper over a turn-based strategic model. CC's classic real-time-with-pause model needs a `TimeModel` that ticks autonomously and allows the player to pause for orders. D&D needs scene-level turns at the strategic level and initiative-order turns inside combat sub-sims. The `TimeModel` abstraction has to support all three at *both* the strategic and sub-sim levels independently.
- **Static vs generated content.** OT proves the static path. D&D proves the generated path. CC will probably stay mostly static but might use LLM generation for variety. The `Director` abstraction has to support all three campaigns without forking the engine.
- **Bidirectional traversal.** OT only moves forward. CC moves freely. D&D moves freely *and* generates new nodes as it goes. The `NodeGraph` abstraction supports all three; the rule pack constrains traversal predicates.
- **Per-Agent control.** OT's `Crew` is mostly passive (you don't issue orders to individual settlers). CC's pilots get individually controlled in tactical missions. D&D's PCs are individually controlled in combat sub-sims and roleplay scenes. The `Agent` data model leaves room for an `assignableTo` field and a `controlMode` so per-campaign code can attach controls to specific agents.

### 16.2 Where it would break (early warnings)

- **Multi-vessel ownership.** CC has multiple `Vessel`s the player builds over time. OT has exactly one. The `Vessel` abstraction is a roster, not a singleton, even though the OT slice's roster has length one.
- **DM safety boundary.** The `LLMDirector` cannot have unmediated write access to game state. Every LLM output is validated against schemas before it touches `GameSession`. If a D&D player asks the DM to "give me a +5 vorpal sword," the DM can narrate that — but the actual inventory mutation has to pass through the loot-distribution schema, which is bounded by level and party size. This is the *bounded GM* pillar from the project docs, enforced architecturally.
- **Sub-sim ⇄ strategic state.** A CC tactical engagement may run for several minutes of real time while the strategic clock pauses. If the sub-sim wants to display HUD info (carrier hull, fuel remaining), it has to read strategic state. The contract is *read-only from strategic, write-via-result at exit*. No partial writes during the sub-sim. This keeps autosave coherent.

If a future Carrier Command or D&D pass reveals an abstraction that does not fit, the answer is to refine the abstraction now, not to fork the engine. That's the contract this doc is making.

---

## 17. Open questions

Deliberately left unresolved by this doc. Filled in during the simulation-layer build, with a balance sweep, or in a later design pass.

### Tuning
- [ ] Exact resource burn rates per travel day (food, water, ammo on hunt, etc.).
- [ ] Exact starting amounts at Independence.
- [ ] Exact store prices at each fort tier (Kearny vs Laramie vs Bridger).

### Slice scope
- [ ] Whether **morale** is its own first-class resource or derived from food + health + recent event outcomes.
- [ ] Whether **oxen** are modeled as a `Resource` quantity or a tiny `Crew` of two `Agent`s.
- [ ] Whether the slice ships with **one fork** (just Sublette vs Bridger) or **two** (also The Dalles raft-vs-bypass).
- [ ] What the minimum fun version of the **hunting** sub-sim includes beyond aim, fire, ammo spend, and food reward.
- [ ] Whether **autosave** writes after every checkpoint (proposed default) or every travel day.
- [ ] Whether **dark mode** is the only mode in the slice or a settings-toggle from day one.

### Sub-simulations
- [ ] What renderer the OT hunting sub-sim uses (RN `<Image>` + `Animated` vs. Skia vs. something else).
- [ ] How much internal hunting state is worth saving versus resolving an interrupted hunt as an aborted result.
- [ ] Which future sub-sims require full interruption recovery instead of the slice's lightweight hunt fallback.
- [ ] Whether sub-sims can themselves launch nested sub-sims, or whether the loop is strictly one level deep.

### LLM director
- [ ] Which model the `LLMDirector` defaults to, and how the choice is exposed (settings toggle vs. per-campaign config).
- [ ] How the per-decision and per-session cost budgets are surfaced to the player (always visible, only-when-near-cap, hidden).
- [ ] What the static fallback library looks like for an LLM-driven D&D campaign — how thin can the baked content be before degraded mode is unplayable.
- [ ] Whether `LLMDirector` runs on-device (mobile-class model) or server-side. Affects offline play, latency, cost, and the "the game must remain fully playable with no network" pillar.
- [ ] What schema validation framework wraps the LLM output (Zod? hand-rolled? something else).

### Content
- [ ] What the **named party members** are called and what their portraits look like.
- [ ] Whether the **map** ships as a single pre-rendered `map_background.png` or assembles from `map_terrain_*.png` tiles.
- [ ] Whether the player can **inspect a logbook** of past decisions, event outcomes, and sub-sim results during a run.
- [ ] Whether **sharable run summaries** ship in the slice or in a follow-up.

---

*End of doc. Re-read in twenty minutes and decide which sections to revise before any simulation-layer code is written.*
