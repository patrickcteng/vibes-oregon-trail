# Asset List — vibes-oregon-trail

All dimensions listed as **base (1×) canvas pixels**. Export at 1×, 2×, 3× with nearest-neighbor scaling unless marked **3× only**.

Export naming convention:
```
filename.png        ← 1× base
filename@2x.png     ← 2× base
filename@3x.png     ← 3× base
```

See `docs/design-system.md` for palette, tile grid, and PixelLab workflow.

---

## Sprites — Wagon

Path: `assets/images/sprites/wagon/`

- [ ] **wagon_idle.png** `64×40` — Side view, parked. Canvas cover slightly loose. Wheels visible, wooden spokes. Warm browns (`Wood Warm`, `Wood Light`). No motion. Transparent background.

- [ ] **wagon_travel_f01.png** `64×40` — Travel animation frame 1. Wheel spokes at 12 o'clock position. Slight canvas sway (cover shifted 1px up vs idle).

- [ ] **wagon_travel_f02.png** `64×40` — Travel animation frame 2. Wheel spokes at 3 o'clock. Canvas sway neutral.

- [ ] **wagon_travel_f03.png** `64×40` — Travel animation frame 3. Wheel spokes at 6 o'clock. Canvas sway 1px down.

- [ ] **wagon_travel_f04.png** `64×40` — Travel animation frame 4. Wheel spokes at 9 o'clock. Canvas sway neutral.

- [ ] **wagon_damaged.png** `64×40` — One wheel cracked or missing a spoke. Canvas torn on one side. Slight lean. Same palette, more `Stone Dark` shadow. Transparent background.

- [ ] **wagon_destroyed.png** `64×40` — Wagon visibly broken down. Collapsed axle. Canvas hanging off. Desaturated. Transparent background.

---

## Sprites — Oxen

Path: `assets/images/sprites/oxen/`

- [ ] **oxen_healthy_f01.png** `48×24` — Pair of oxen, side view, yoked together. Frame 1 of walk cycle: left front leg forward. Brown with white patches. Transparent background.

- [ ] **oxen_healthy_f02.png** `48×24` — Walk cycle frame 2: neutral stance.

- [ ] **oxen_healthy_f03.png** `48×24` — Walk cycle frame 3: right front leg forward.

- [ ] **oxen_healthy_f04.png** `48×24` — Walk cycle frame 4: neutral stance.

- [ ] **oxen_exhausted.png** `48×24` — Both oxen heads drooped, slow posture. No animation frames needed — single static sprite used when tired. Desaturated slightly. Transparent background.

- [ ] **oxen_dead.png** `48×24` — Oxen lying on side. Horizontal position. Fully desaturated. Transparent background.

---

## Sprites — Party Members

Path: `assets/images/sprites/party/`

Each party member has 3 health states. Design one generic settler; the game tints or recolors slightly per character if needed.

- [ ] **party_healthy_idle.png** `16×32` — Front-facing settler. 1840s trail clothes: wide-brim hat, coat, boots. Neutral expression. Standing straight. Transparent background.

- [ ] **party_healthy_walk_f01.png** `16×32` — Walk frame 1: left leg forward.

- [ ] **party_healthy_walk_f02.png** `16×32` — Walk frame 2: neutral.

- [ ] **party_sick.png** `16×32` — Same settler, pallor green tint, hunched forward 2px. No walk animation needed for sick state. Transparent background.

- [ ] **party_dead.png** `32×16` — Settler lying horizontal, eyes closed, hat beside them. Somber. Desaturated. Transparent background.

---

## Sprites — NPCs

Path: `assets/images/sprites/npc/`

- [ ] **npc_shopkeeper.png** `24×40` — Friendly store owner. Apron, rolled sleeves, slight smile. Standing behind counter implied (crop at waist). Transparent background.

- [ ] **npc_trapper.png** `24×40` — Grizzled trail figure. Fur hat, heavy coat. Used for info/event encounters. Transparent background.

---

## Landmarks — Scene Art

Path: `assets/images/landmarks/`

All landmark scenes are **3× only** (no @2x or @1x needed). Full canvas width.

Base size: `320×128`. Export: `960×384` at 3×.

- [ ] **landmark_independence.png** `320×128` — Missouri frontier town, 1848. Wooden storefronts, hitching posts, wagons assembling. Warm morning light. Bustling but rustic. Sky blue upper third.

- [ ] **landmark_kansas_crossing.png** `320×128` — Wide muddy river, shallow ford. Wagon mid-crossing, water at wheel hubs. Far bank visible. Brown water, blue sky. Tension in the composition.

- [ ] **landmark_fort_kearny.png** `320×128` — Flat plains fort. Wooden palisade walls, single gate, small US flag. Sparse trees. Wide open sky. Dusty brown palette.

- [ ] **landmark_chimney_rock.png** `320×128` — Iconic spire rock formation rising dramatically from flat Nebraska plains. Travelers in silhouette at base for scale. Warm orange sky.

- [ ] **landmark_fort_laramie.png** `320×128` — More established fort. Adobe and stone buildings, mountain backdrop in distance. Slightly greener terrain than Kearny.

- [ ] **landmark_independence_rock.png** `320×128` — Large smooth dome of granite in open plain. Names carved visible on surface. Bright midday light. Some scattered travelers camped nearby.

- [ ] **landmark_south_pass.png** `320×128` — Wide mountain valley, low pass between snowy peaks. Trail clearly visible winding through. Cooler palette, late afternoon light.

- [ ] **landmark_fort_bridger.png** `320×128` — Small trading post in high terrain. Log buildings, mountain backdrop. More isolated feel than Laramie.

- [ ] **landmark_snake_river.png** `320×128` — Turbulent river, rocky narrow crossing or dangerous ford. Dark rushing water, steep rocky banks. Threatening composition.

- [ ] **landmark_blue_mountains.png** `320×128` — Dense pine forest on steep terrain. Trail barely visible cutting through trees. Cool greens and shadows. Atmospheric haze in distance.

- [ ] **landmark_the_dalles.png** `320×128` — Columbia River canyon. Dramatic cliffs, wide river below. The end of the overland trail — either raft or mountain bypass decision.

- [ ] **landmark_willamette_valley.png** `320×128` — Lush green arrival valley. Farmland, trees, river. Warm golden sunset. Victory scene energy. Richest greens in the entire palette.

---

## Map — Route Overview

Path: `assets/images/map/`

The map view. **3× only**.

- [ ] **map_background.png** `320×568` — Full canvas parchment-texture route map. Oregon Trail route as a dotted/dashed line from lower-right (Independence MO) curving up to upper-left (Willamette Valley). Hand-drawn style geography, minimal labels. Aged tan paper look (`Parchment`). No node markers — those are overlaid by the engine.

- [ ] **map_terrain_plains.png** `32×32` — Tileable plains texture for map background regions. Tiny grass tufts, flat. Warm tan.

- [ ] **map_terrain_mountains.png** `32×32` — Tileable mountain terrain tile. Small jagged peaks silhouette. Grey-blue.

- [ ] **map_terrain_forest.png** `32×32` — Tileable forest tile. Tiny tree tops. Dark green.

- [ ] **map_terrain_river.png** `32×32` — Tileable river segment. Wavy blue horizontal band.

### Map Nodes — `16×16`, all three scale variants

Path: `assets/images/map/nodes/`

- [ ] **node_unvisited.png** `16×16` — Small empty circle. Muted `Stone Light`. Transparent background.

- [ ] **node_current.png** `16×16` — Filled circle with glow/pulse halo. `Gold` or `Cream`. Transparent background.

- [ ] **node_visited.png** `16×16` — Filled circle, faded. `Grey Muted`. Transparent background.

- [ ] **node_fort.png** `16×16` — Tiny fort icon. `Wood Warm` walls, tiny flag. Transparent background.

- [ ] **node_crossing.png** `16×16` — Wavy blue line (river) with a small crossing arrow. Transparent background.

- [ ] **node_mountain.png** `16×16` — Small jagged peak silhouette. `Stone Mid`. Transparent background.

- [ ] **node_town.png** `16×16` — Tiny building with chimney. `Wood Warm`. Transparent background.

---

## Icons — Inventory

Path: `assets/images/icons/inventory/`

All `16×16`. All three scale variants. Transparent background. Clean, readable at small size — silhouette must read clearly at 1×.

- [ ] **icon_food.png** `16×16` — Smoked/dried meat bundle. Earthy brown, slight shine highlight.

- [ ] **icon_water.png** `16×16` — Wooden barrel with blue tint overtone. Small water droplet on side.

- [ ] **icon_medicine.png** `16×16` — Small brown bottle, cork top. Tiny white cross or label.

- [ ] **icon_ammunition.png** `16×16` — Three small bullets stacked or a powder horn. Dark metal grey.

- [ ] **icon_clothing.png** `16×16` — Folded coat or shirt. Warm brown-grey.

- [ ] **icon_wagon_parts.png** `16×16` — Spare wagon wheel, side view. `Wood Warm` spokes.

- [ ] **icon_money.png** `16×16` — Small coin stack. `Gold` with `Stone Dark` shadow edge.

- [ ] **icon_oxen.png** `16×16` — Single ox head, side view. Brown, simple readable silhouette.

- [ ] **icon_tools.png** `16×16` — Hammer or axe. `Stone Mid` head, `Wood Warm` handle.

---

## Icons — Status

Path: `assets/images/icons/status/`

All `16×16`. All three scale variants. Transparent background.

- [ ] **status_healthy.png** `16×16` — Solid green heart. `Green Good`.

- [ ] **status_hungry.png** `16×16` — Empty bowl with fork. `Yellow Alert` tones.

- [ ] **status_sick.png** `16×16` — Skull or green face. `Green Mid` / `Grey Muted`.

- [ ] **status_injured.png** `16×16` — Bandage cross. `Red Danger` cross on `Cream` bandage.

- [ ] **status_exhausted.png** `16×16` — "Zzz" in small pixel letters, or drooping eye. `Grey Muted`.

- [ ] **status_dead.png** `16×16` — Tombstone silhouette. `Stone Mid`.

- [ ] **status_morale_high.png** `16×16` — Raised fist or smiley face. `Gold`.

- [ ] **status_morale_low.png** `16×16` — Frowning face. `Grey Muted`.

- [ ] **status_morale_critical.png** `16×16` — Cracked heart or angry face. `Red Danger`.

---

## Event Art

Path: `assets/images/events/`

Event card background scenes. `160×96`. **3× only** (`480×288` export). These appear behind event text in the event resolution screen.

- [ ] **event_storm.png** `160×96` — Dark churning sky, lightning bolt striking, heavy rain lines. Threatening. `Sky Deep`, `Stone Dark`, `Water Light` for rain streaks.

- [ ] **event_illness.png** `160×96` — Dim wagon interior. Lantern casting warm glow. Party member shape lying under blanket. Intimate, somber.

- [ ] **event_broken_wheel.png** `160×96` — Roadside scene. Wagon tilted, one wheel cracked on trail. Tools scattered on ground.

- [ ] **event_river_flood.png** `160×96` — River swollen above banks. Brown water rushing, debris floating. Near-crossing panic energy.

- [ ] **event_good_hunting.png** `160×96` — Open sunny plains. Deer or bison silhouettes in mid-distance. Blue sky, green grass. Hopeful.

- [ ] **event_harsh_weather.png** `160×96` — Blinding snowstorm or dust storm. Near-whiteout or tan haze. Barely-visible wagon outline.

- [ ] **event_lost_trail.png** `160×96` — Dense forest, forked path, no clear markers. Dusk light through trees. Uncertain.

- [ ] **event_friendly_encounter.png** `160×96` — Peaceful meeting on trail. Two groups, exchange of goods. Warm midday light.

- [ ] **event_theft.png** `160×96` — Shadowy silhouettes on ridge above trail at night. Campfire visible below. Tense.

- [ ] **event_good_rest.png** `160×96` — Campfire scene, clear night sky with stars, wagon resting nearby. Peaceful.

- [ ] **event_find_supplies.png** `160×96` — Abandoned cache by trail. Crates and barrels half-buried or stacked. Lucky find energy.

---

## Store

Path: `assets/images/store/`

- [ ] **store_background.png** `320×160` — Frontier general store interior. Wood plank walls, shelves of goods (barrels, boxes, hanging items), wooden counter. Warm lantern light. **3× only**.

- [ ] **store_counter.png** `160×32` — Just the counter top, for overlay compositing if needed. Wood grain surface. **3× only**.

---

## UI — Panels and Chrome

Path: `assets/images/ui/`

- [ ] **panel_frame_corner_tl.png** `8×8` — Top-left corner of 9-slice panel border. Wood/rope texture. All three scale variants.

- [ ] **panel_frame_corner_tr.png** `8×8` — Top-right corner. Mirror of TL.

- [ ] **panel_frame_corner_bl.png** `8×8` — Bottom-left corner.

- [ ] **panel_frame_corner_br.png** `8×8` — Bottom-right corner.

- [ ] **panel_frame_edge_top.png** `8×8` — Top edge tile (tileable horizontally). Rope or wood beam. All three scale variants.

- [ ] **panel_frame_edge_bottom.png** `8×8` — Bottom edge tile.

- [ ] **panel_frame_edge_left.png** `8×8` — Left edge tile (tileable vertically).

- [ ] **panel_frame_edge_right.png** `8×8` — Right edge tile.

- [ ] **panel_fill_dark.png** `8×8` — Dark panel fill tile. `UI Dark` with subtle grain. Tileable.

- [ ] **panel_fill_parchment.png** `8×8` — Parchment panel fill tile. `Parchment` with subtle grain. Tileable.

- [ ] **button_normal.png** `80×16` — Button face. `Stone Mid` with `Stone Light` top-left pixel highlight, `Stone Dark` bottom-right shadow. All three scale variants.

- [ ] **button_pressed.png** `80×16` — Button face pressed state. Inverted highlights, slightly darker fill.

- [ ] **button_disabled.png** `80×16` — Button face disabled. `Grey Muted` fill, no highlights.

- [ ] **divider_horizontal.png** `320×4` — Horizontal divider line. Rope or wood grain texture. **3× only**.

- [ ] **scroll_bg.png** `160×80` — Parchment scroll texture for text areas. Aged, slightly rolled edges. **3× only**.

---

## UI — HUD

Path: `assets/images/ui/hud/`

All three scale variants.

- [ ] **hud_bar_track.png** `64×8` — Empty resource bar track. `UI Dark` with inner shadow edge. No fill — fill is drawn programmatically.

- [ ] **hud_bar_fill_health.png** `64×8` — Health bar fill. Solid `Red Bright`. Tileable on X axis.

- [ ] **hud_bar_fill_food.png** `64×8` — Food bar fill. `Dirt Light`. Tileable.

- [ ] **hud_bar_fill_water.png** `64×8` — Water bar fill. `Water Light`. Tileable.

- [ ] **hud_bar_fill_money.png** `64×8` — Money bar fill. `Gold`. Tileable.

- [ ] **hud_bar_fill_morale.png** `64×8` — Morale bar fill. `Yellow Alert`. Tileable.

- [ ] **hud_bar_fill_wagon.png** `64×8` — Wagon condition bar fill. `Wood Warm`. Tileable.

- [ ] **hud_portrait_frame.png** `24×24` — Portrait frame border for party member avatar slot. Matches panel border style.

---

## Weather Overlays

Path: `assets/images/weather/`

Transparent overlay tiles. Applied over game scenes by engine. **3× only**. `64×64`, tileable on both axes.

- [ ] **weather_rain.png** `64×64` — Diagonal streaks, upper-left to lower-right. `Water Light` at ~40% opacity. Semi-transparent PNG.

- [ ] **weather_heavy_rain.png** `64×64` — Denser diagonal streaks, slightly wider. `Water Mid` at ~60% opacity.

- [ ] **weather_snow.png** `64×64` — Small round dots scattered, slightly varied sizes. White at ~50% opacity.

- [ ] **weather_dust.png** `64×64` — Horizontal haze bands. `Dirt Pale` at ~50% opacity. Desert/plains feel.

- [ ] **weather_fog.png** `64×64` — Dense soft haze. `Sky Pale` at ~55% opacity. Flat fill with slight density variation.

---

## Full Screens

Path: `assets/images/screens/`

**3× only**. `320×568` canvas size. Export at `960×1704`.

- [ ] **screen_title.png** `320×568` — Title screen. Wagon silhouette on trail at sunset, dramatic sky. Game logo space at top third. Rich warm colors. Cinematic for a pixel game.

- [ ] **screen_victory.png** `320×568` — Wagon arriving in Willamette Valley. Green rolling hills, warm gold sky, farmland. Triumphant. Party figures celebrating in foreground.

- [ ] **screen_gameover.png** `320×568` — Desolate trail, single tombstone, abandoned wagon in distance. Desaturated, cool blue-grey. Somber. Spare.

- [ ] **screen_loading.png** `320×568` — Simple animated loading frame (or single static frame). Trail scene with "wagon wheel spinning" implication. Minimal.

---

## Checklist Summary

**Total assets: 98**

| Category           | Count | Done |
|--------------------|-------|------|
| Wagon sprites      | 7     |      |
| Oxen sprites       | 6     |      |
| Party sprites      | 6     |      |
| NPC sprites        | 2     |      |
| Landmark scenes    | 12    |      |
| Map background     | 5     |      |
| Map nodes          | 7     |      |
| Inventory icons    | 9     |      |
| Status icons       | 9     |      |
| Event art          | 11    |      |
| Store art          | 2     |      |
| UI panels/chrome   | 16    |      |
| UI HUD             | 8     |      |
| Weather overlays   | 5     |      |
| Full screens       | 4     |      |

---

## Questions / Open Items

- [ ] Do we want directional facing sprites (left/right) for party members, or flip horizontally in code?
- [ ] Does the map use pre-rendered terrain tiles or is the background one static image?
- [ ] Do landmark scenes animate (parallax layers) or are they static?
- [ ] Are event card backgrounds reused across similar event types, or unique per event?
- [ ] How many distinct party member appearances do we want (same base sprite recolored, or multiple designs)?
