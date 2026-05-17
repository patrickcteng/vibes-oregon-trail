# PixelLab Prompt Pack

Copy-paste prompts for the assets in `docs/asset-list.md`.

These prompts are tuned for a text-first PixelLab workflow and aligned to `docs/design-system.md`.

## Global PixelLab Settings

Use these defaults unless an asset entry says otherwise:

- Style anchor: `clean retro 16-bit inspired pixel art, late 80s to early 90s console game look, SNES and Genesis homage, crisp readable game asset, limited 32-color palette, no anti-aliasing, no blur, clean silhouette, nearest-neighbor look`
- If an entry includes a `Direction` line, set PixelLab's direction control to that exact value. Do not rely on the prompt alone for camera angle.
- If an entry does not include a `Direction` line, leave Direction on `None`.
- For non-square assets, generate on the smallest square PixelLab canvas that fully contains the final asset, then crop the final PNG back to the repo spec size.
- Keep the subject composed inside the final export area, with the extra square-canvas padding left empty or transparent where possible.
- Export at base size first, then scale to `@2x` and `@3x` with integer nearest-neighbor scaling only.
- For sprites, icons, UI pieces, and overlays: generate as isolated assets with a transparent background if PixelLab supports it. If not, use a flat solid backdrop for easy cleanup.
- For animation sets: treat the first frame as the style anchor, then reuse the result as an init image or inpaint source for later frames.
- For inpainting: describe the full visible image, not just the masked region, so PixelLab keeps the rest coherent.
- Keep the master palette locked to the colors in `docs/design-system.md`. Do not introduce extra colors.

## Shared Negative Prompt

Use this whenever the entry does not need extra exclusions:

`blurry, anti-aliased edges, painterly shading, watercolor, smooth gradients, 3D render, photorealistic, modern mobile app aesthetic, vector art, text, letters, watermark, logo, frame crop, off-palette neon colors, noisy background, extra objects, wrong perspective, high detail realism`

## Sprites — Wagon

### wagon_idle.png
PixelLab generation size: `64x64`
Final export size: `64x40`
Path: `assets/images/sprites/wagon/`
Direction: `West`

Prompt:
`pixel art game sprite, strict orthographic side profile prairie wagon facing left, 64x40 canvas, isolated wagon only, transparent background, full wagon visible, two wooden wheels seen directly from the side with clear spokes, slightly loose covered canvas top, warm wood warm and wood light browns, stone dark shadow, frontier trail vehicle, crisp pixels, readable silhouette, no motion, no ground, centered with a little breathing room`

Negative prompt:
`three quarter view, angled view, front view, top-down view, isometric, perspective camera, people, oxen, scenery, ground plane, blur, anti-aliased outline, extra cargo, cropped wheels`

PixelLab notes:
Use this as the visual anchor for all wagon variants. Reuse it as an init image for travel, damaged, and destroyed states.

### wagon_travel_f01.png
PixelLab generation size: `64x64`
Final export size: `64x40`
Path: `assets/images/sprites/wagon/`
Direction: `West`

Prompt:
`same wagon silhouette, same strict orthographic side profile facing left, same palette and proportions as wagon_idle, 64x40 transparent background, travel animation frame 1, wheels seen directly from the side, spokes rotated to 12 oclock, subtle bounce, canvas cover shifted up by 1 pixel, crisp readable sprite, no new details`

Negative prompt:
`new wagon design, different camera angle, extra props, motion blur, oxen, ground, background`

PixelLab notes:
Use `wagon_idle` as the init image. Keep all changes limited to wheel rotation and a slight upward sway.

### wagon_travel_f02.png
PixelLab generation size: `64x64`
Final export size: `64x40`
Path: `assets/images/sprites/wagon/`
Direction: `West`

Prompt:
`same wagon silhouette, same strict orthographic side profile facing left, same palette and proportions as wagon_idle, 64x40 transparent background, travel animation frame 2, wheels seen directly from the side, spokes rotated to 3 oclock, canvas sway neutral, rolling forward, clean pixel art sprite, no extra movement besides wheel rotation and subtle travel posture`

Negative prompt:
`different wagon, perspective shift, blur, extra scenery, oxen, exaggerated bounce`

PixelLab notes:
Use the same init image chain as frame 1 so the wagon does not drift.

### wagon_travel_f03.png
PixelLab generation size: `64x64`
Final export size: `64x40`
Path: `assets/images/sprites/wagon/`
Direction: `West`

Prompt:
`same wagon silhouette, same strict orthographic side profile facing left, same palette and proportions as wagon_idle, 64x40 transparent background, travel animation frame 3, wheels seen directly from the side, spokes rotated to 6 oclock, canvas cover shifted down by 1 pixel, subtle downward sway, rolling trail wagon sprite`

Negative prompt:
`new details, broken wheel, oxen, people, blur, soft shading, background`

PixelLab notes:
Keep the body identical to frame 1 and 2 except for the planned wheel and cover movement.

### wagon_travel_f04.png
PixelLab generation size: `64x64`
Final export size: `64x40`
Path: `assets/images/sprites/wagon/`
Direction: `West`

Prompt:
`same wagon silhouette, same strict orthographic side profile facing left, same palette and proportions as wagon_idle, 64x40 transparent background, travel animation frame 4, wheels seen directly from the side, spokes rotated to 9 oclock, neutral canvas sway, readable pixel art rolling wagon`

Negative prompt:
`camera change, extra objects, blur, oxen, scenery, dramatic tilt`

PixelLab notes:
This should loop cleanly back into frame 1.

### wagon_damaged.png
PixelLab generation size: `64x64`
Final export size: `64x40`
Path: `assets/images/sprites/wagon/`
Direction: `West`

Prompt:
`same base wagon as wagon_idle, strict orthographic side profile facing left, 64x40 transparent background, damaged frontier wagon sprite, one wheel cracked or missing a spoke, canvas torn on one side, wagon leaning slightly, same warm wood palette with heavier stone dark shadows, still readable and usable in gameplay, not fully destroyed`

Negative prompt:
`complete wreckage, fire, people, oxen, background landscape, top-down, photoreal detail`

PixelLab notes:
Keep it visually tied to the idle wagon. Damage should feel repairable.

### wagon_destroyed.png
PixelLab generation size: `64x64`
Final export size: `64x40`
Path: `assets/images/sprites/wagon/`
Direction: `West`

Prompt:
`same base wagon silhouette as wagon_idle, strict orthographic side profile facing left, 64x40 transparent background, destroyed wagon sprite, collapsed axle, hanging torn canvas, broken frame, one wheel displaced or collapsed, desaturated wood and grey muted tones, somber readable silhouette, clearly unusable`

Negative prompt:
`explosion, fire, gore, background scene, people, oxen, clean intact wagon`

PixelLab notes:
Push the collapse and desaturation harder than `wagon_damaged` while preserving recognizability.

## Sprites — Oxen

### oxen_healthy_f01.png
PixelLab generation size: `64x64`
Final export size: `48x24`
Path: `assets/images/sprites/oxen/`
Direction: `West`

Prompt:
`pixel art game sprite, strict orthographic side profile oxen pair facing left, 48x24 canvas, transparent background, two yoked oxen only, brown bodies with white patches, clear shared yoke, both animals seen directly from the side, left front leg forward for walk cycle frame 1, compact readable silhouette, frontier travel animal sprite`

Negative prompt:
`single ox, front view, top-down, realistic fur texture, people, wagon, grass, blur, extra limbs`

PixelLab notes:
This is the anchor for all healthy oxen frames. Keep body proportions identical across frames.

### oxen_healthy_f02.png
PixelLab generation size: `64x64`
Final export size: `48x24`
Path: `assets/images/sprites/oxen/`
Direction: `West`

Prompt:
`same oxen pair, same strict orthographic side profile facing left, same palette and proportions as oxen_healthy_f01, 48x24 transparent background, walk cycle frame 2, neutral stance, both animals balanced under the yoke, crisp readable pixel sprite`

Negative prompt:
`new ox design, wagon, scenery, blur, different yoke, exaggerated motion`

PixelLab notes:
Use frame 1 as the init image and adjust only leg positions.

### oxen_healthy_f03.png
PixelLab generation size: `64x64`
Final export size: `48x24`
Path: `assets/images/sprites/oxen/`
Direction: `West`

Prompt:
`same oxen pair, same strict orthographic side profile facing left, same palette and proportions as oxen_healthy_f01, 48x24 transparent background, walk cycle frame 3, right front leg forward, yoked together, readable small sprite with slight forward motion energy`

Negative prompt:
`camera change, extra scenery, blur, new markings, different colors, wagon`

PixelLab notes:
Mirror the energy of frame 1 without changing the silhouette family.

### oxen_healthy_f04.png
PixelLab generation size: `64x64`
Final export size: `48x24`
Path: `assets/images/sprites/oxen/`
Direction: `West`

Prompt:
`same oxen pair, same strict orthographic side profile facing left, same palette and proportions as oxen_healthy_f01, 48x24 transparent background, walk cycle frame 4, neutral stance, clean loop back toward frame 1`

Negative prompt:
`running, leaping, blur, different camera angle, background, extra props`

PixelLab notes:
Keep it close to frame 2 so the cycle feels stable.

### oxen_exhausted.png
PixelLab generation size: `64x64`
Final export size: `48x24`
Path: `assets/images/sprites/oxen/`
Direction: `West`

Prompt:
`same oxen pair design as healthy frames, strict orthographic side profile facing left, 48x24 transparent background, exhausted yoked oxen, both heads drooped, shoulders lowered, slow tired posture, slightly desaturated browns and greys, readable fatigue at small size`

Negative prompt:
`dead oxen, running, dramatic collapse, wagon, scenery, blur`

PixelLab notes:
This should look depleted but still alive and standing.

### oxen_dead.png
PixelLab generation size: `64x64`
Final export size: `48x24`
Path: `assets/images/sprites/oxen/`
Direction: `None`

Prompt:
`same oxen pair design as healthy frames, 48x24 transparent background, oxen dead and lying on their side, strict side profile body shapes, horizontal composition, fully desaturated grey muted and stone tones, somber readable silhouette, frontier animal loss sprite`

Negative prompt:
`blood, gore, standing oxen, wagon, background, realism, extra debris`

PixelLab notes:
Keep it clean and game-appropriate. The silhouette should still read instantly at small size.

## Sprites — Party Members

### party_healthy_idle.png
PixelLab generation size: `64x64`
Final export size: `16x32`
Path: `assets/images/sprites/party/`
Direction: `South`

Prompt:
`pixel art character sprite, straight front view settler facing camera, 16x32 canvas, transparent background, one generic 1840s trail traveler, wide brim hat, simple coat, pants, boots, neutral expression, standing upright, centered, compact readable silhouette, earthy browns and muted cloth colors, designed for recolor variations later`

Negative prompt:
`side view, modern clothes, fantasy armor, large face detail, blur, background scenery, weapon, extra accessories`

PixelLab notes:
Use this as the base for walk and sick variants. Keep forms very simple because the sprite is tiny.

### party_healthy_walk_f01.png
PixelLab generation size: `64x64`
Final export size: `16x32`
Path: `assets/images/sprites/party/`
Direction: `South`

Prompt:
`same settler design, palette, and straight front view as party_healthy_idle, 16x32 transparent background, walk frame 1, left leg forward, slight arm swing, same hat and coat silhouette, clean readable pixel animation frame`

Negative prompt:
`side view, new clothing, blur, large motion smear, scenery, extra gear`

PixelLab notes:
Use the idle sprite as the init image and shift limbs conservatively.

### party_healthy_walk_f02.png
PixelLab generation size: `64x64`
Final export size: `16x32`
Path: `assets/images/sprites/party/`
Direction: `South`

Prompt:
`same settler design, palette, and straight front view as party_healthy_idle, 16x32 transparent background, walk frame 2, neutral centered stance, slight walking rhythm, same hat and coat silhouette, crisp readable pixel sprite`

Negative prompt:
`camera shift, different outfit, blur, scenery, oversized head`

PixelLab notes:
Keep this very close to idle so the loop remains stable.

### party_sick.png
PixelLab generation size: `64x64`
Final export size: `16x32`
Path: `assets/images/sprites/party/`
Direction: `South`

Prompt:
`same settler design as party_healthy_idle, straight front view facing camera, 16x32 transparent background, sick trail traveler, pallor green tint in face and clothing shadows, hunched forward by about 2 pixels, tired posture, subdued expression, still readable and humane, no animation`

Negative prompt:
`zombie, gore, dramatic horror, healthy confident pose, blur, background`

PixelLab notes:
Preserve the same clothing and proportions as the healthy sprite.

### party_dead.png
PixelLab generation size: `64x64`
Final export size: `32x16`
Path: `assets/images/sprites/party/`
Direction: `None`

Prompt:
`same settler design as party_healthy_idle, 32x16 transparent background, dead trail traveler lying horizontally, side profile body shape, eyes closed, hat placed beside the body, desaturated muted browns and greys, somber but respectful, simple readable silhouette`

Negative prompt:
`gore, blood, standing pose, background, extra props, dramatic realism`

PixelLab notes:
Keep this understated and game-appropriate.

## Sprites — NPCs

### npc_shopkeeper.png
PixelLab generation size: `64x64`
Final export size: `24x40`
Path: `assets/images/sprites/npc/`
Direction: `South`

Prompt:
`pixel art npc sprite, straight front view facing camera, 24x40 canvas, transparent background, friendly frontier shopkeeper, apron, rolled sleeves, slight smile, cropped around waist as if standing behind a counter, readable face and silhouette, warm browns and cream highlights`

Negative prompt:
`full body legs, modern shop clerk, fantasy merchant, background, counter included, blur, extra goods`

PixelLab notes:
Keep enough personality to stand out from party members without becoming overly detailed.

### npc_trapper.png
PixelLab generation size: `64x64`
Final export size: `24x40`
Path: `assets/images/sprites/npc/`
Direction: `South`

Prompt:
`pixel art npc sprite, straight front view facing camera, 24x40 canvas, transparent background, grizzled trapper or trail scout, fur hat, heavy coat, weathered expression, frontier ruggedness, readable silhouette, muted earth palette, suitable for encounters and guidance scenes`

Negative prompt:
`full background, weapon focus, fantasy hunter, modern winter gear, blur, over-detailed realism`

PixelLab notes:
Make the figure feel more severe than the shopkeeper but still consistent with the same world.

## Landmarks — Scene Art

### landmark_independence.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, Independence Missouri frontier town in 1848, wooden storefronts, hitching posts, a few wagons assembling, bustling but rustic main street, warm morning light, sky mid and sky light upper third, readable town silhouettes, no text, composition designed as a wide mobile banner`

Negative prompt:
`modern city, realistic painting, text labels, photoreal storefronts, blur, overcrowded detail, fantasy buildings`

PixelLab notes:
Leave the lower portion readable for UI overlays if needed. These landmark scenes are 3x-only exports.

### landmark_kansas_crossing.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, wide muddy river crossing on the frontier, wagon mid crossing with water at wheel hubs, far bank visible, brown water, blue sky, strong tension in the composition, shallow ford but risky, readable silhouettes and water motion`

Negative prompt:
`bridge, modern boat, photoreal water, text, blur, top-down map view`

PixelLab notes:
Push tension through angle and current, not through clutter.

### landmark_fort_kearny.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, Fort Kearny on flat plains, wooden palisade walls, single gate, tiny US flag, sparse trees, wide open dusty sky, dusty brown palette with wood warm structures, frontier fort outpost`

Negative prompt:
`stone castle, modern fort, crowded town, blur, fantasy towers, text`

PixelLab notes:
Keep the fort simple and broad, with lots of sky and plains space.

### landmark_chimney_rock.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, dramatic chimney rock spire rising from flat Nebraska plains, tiny travelers and wagon silhouettes at the base for scale, warm orange sky, iconic geological landmark, strong vertical silhouette against a simple background`

Negative prompt:
`forest canyon, photoreal rock texture, text, blur, cluttered foreground, modern hikers`

PixelLab notes:
The spire should dominate the composition immediately.

### landmark_fort_laramie.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, Fort Laramie with adobe and stone buildings, more established than earlier forts, slight greenery, distant mountains in the background, frontier outpost with broader settlement feel, clear daylight`

Negative prompt:
`medieval fort, modern buildings, blur, text signs, dense city street`

PixelLab notes:
Make it feel more developed than Fort Kearny without losing the frontier atmosphere.

### landmark_independence_rock.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, large smooth granite dome in open plains, carved names faintly visible on the rock surface, bright midday light, a few small travelers camped nearby, huge landmark mass dominating the scene`

Negative prompt:
`sharp mountain peak, photoreal granite, modern campsite, blur, text overlay`

PixelLab notes:
The rock should read as a giant smooth dome, not a jagged mountain.

### landmark_south_pass.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, broad mountain valley at South Pass, low pass between snowy peaks, visible winding trail, cooler palette, late afternoon light, sweeping open route through high terrain`

Negative prompt:
`tight canyon, fantasy mountains, blur, text, modern road`

PixelLab notes:
Keep the route legible so the scene implies progress through the pass.

### landmark_fort_bridger.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, small isolated trading post in high country, log buildings, mountain backdrop, sparse surroundings, cooler frontier atmosphere, more remote than Fort Laramie`

Negative prompt:
`large town, city street, blur, text, fantasy outpost`

PixelLab notes:
Emphasize isolation and altitude.

### landmark_snake_river.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, turbulent Snake River crossing, dark rushing water, rocky steep banks, narrow dangerous passage, threatening composition, water dark and water foam accents, frontier peril`

Negative prompt:
`calm lake, bridge, photoreal rapids, text, blur, modern raft`

PixelLab notes:
The danger should come from current and terrain, not from visual noise.

### landmark_blue_mountains.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, dense blue mountains forest, steep slopes with dark pine trees, narrow trail barely visible, cool greens, deep shadows, distant atmospheric haze, moody but readable`

Negative prompt:
`tropical jungle, photoreal mist, text, blur, bright cheerful meadow`

PixelLab notes:
Keep the trail faint but readable enough to suggest difficult progress.

### landmark_the_dalles.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, Columbia River canyon at The Dalles, dramatic cliffs, wide river below, sense of decision point between raft route and mountain bypass, expansive canyon composition, frontier endgame location`

Negative prompt:
`modern dam, city skyline, blur, text labels, fantasy canyon colors`

PixelLab notes:
Make the geography feel consequential and strategic.

### landmark_willamette_valley.png
PixelLab generation size: `320x320`
Final export size: `320x128`
Path: `assets/images/landmarks/`

Prompt:
`retro 16-bit inspired pixel art landmark banner, 320x128 scene, lush Willamette Valley arrival, rich green fields, trees, river, warm golden sunset, fertile farmland, peaceful victory energy, brightest greens in the whole game palette`

Negative prompt:
`barren plains, dark storm, blur, text, modern farm machinery, photorealism`

PixelLab notes:
This should feel like relief and reward after the harsher trail scenes.

## Map — Route Overview

### map_background.png
PixelLab generation size: `576x576`
Final export size: `320x568`
Path: `assets/images/map/`

Prompt:
`retro 16-bit inspired pixel art full screen map, 320x568 portrait canvas, parchment route map of the Oregon Trail style journey, aged tan paper texture, dotted route starting near lower right and curving toward upper left, hand-drawn geography, rivers, mountains, forests, minimal labels or no labels, no node markers, readable on mobile, decorative but functional`

Negative prompt:
`modern GPS map, satellite imagery, crowded text, realistic parchment photo, blur, icons, node markers`

PixelLab notes:
Reserve visual simplicity around the route so engine overlays remain readable.

### map_terrain_plains.png
Size: `32x32`
Path: `assets/images/map/`

Prompt:
`retro 16-bit inspired pixel art tileable plains terrain tile, 32x32, warm tan ground, tiny grass tufts, flat open prairie texture, subtle variation, seamless tiling on all edges`

Negative prompt:
`large landmarks, shadows that break tiling, blur, mountains, river, text`

PixelLab notes:
Ask PixelLab for a repeating texture; plan on manual seam cleanup if needed.

### map_terrain_mountains.png
Size: `32x32`
Path: `assets/images/map/`

Prompt:
`retro 16-bit inspired pixel art tileable mountain terrain tile, 32x32, grey blue jagged peak shapes, map-style terrain texture, small repeated mountain silhouettes, seamless tiling on all edges`

Negative prompt:
`single giant mountain, realistic landscape painting, blur, forests, river`

PixelLab notes:
This is a map texture, not a scenic mountain painting.

### map_terrain_forest.png
Size: `32x32`
Path: `assets/images/map/`

Prompt:
`retro 16-bit inspired pixel art tileable forest terrain tile, 32x32, dark green clustered tree tops, map-style pattern, simple overhead texture look, seamless tiling on all edges`

Negative prompt:
`full scenic forest scene, blur, individual large trunks, river, text`

PixelLab notes:
Favor a simplified map texture over detailed trees.

### map_terrain_river.png
Size: `32x32`
Path: `assets/images/map/`

Prompt:
`retro 16-bit inspired pixel art tileable river terrain tile, 32x32, wavy blue horizontal band, map-style water texture, simple repeated pattern, seamless left and right edges, readable as a river region`

Negative prompt:
`waterfall, scenic lake, blur, photoreal reflections, shorelines`

PixelLab notes:
Keep the pattern broad enough to tile without obvious seams.

## Map Nodes

### node_unvisited.png
Size: `16x16`
Path: `assets/images/map/nodes/`

Prompt:
`clean retro 16-bit inspired pixel art map node icon, 16x16 transparent background, small empty circle, stone light and muted outline, simple readable symbol for unvisited location`

Negative prompt:
`complex scenery, glow, blur, text, square icon`

PixelLab notes:
These icons must read clearly at 1x.

### node_current.png
Size: `16x16`
Path: `assets/images/map/nodes/`

Prompt:
`clean retro 16-bit inspired pixel art map node icon, 16x16 transparent background, filled circle with subtle glow or pulse halo, gold and cream highlight, current location marker, small but prominent`

Negative prompt:
`large effect, blur, text, scenery, realistic light bloom`

PixelLab notes:
Keep the halo pixel-based and contained.

### node_visited.png
Size: `16x16`
Path: `assets/images/map/nodes/`

Prompt:
`clean retro 16-bit inspired pixel art map node icon, 16x16 transparent background, filled circle, faded grey muted tone, simple symbol for visited location`

Negative prompt:
`glow, scenery, blur, text, heavy detail`

PixelLab notes:
Should look quieter than both current and unvisited nodes.

### node_fort.png
Size: `16x16`
Path: `assets/images/map/nodes/`

Prompt:
`clean retro 16-bit inspired pixel art map node icon, 16x16 transparent background, tiny fort symbol, wood warm walls, tiny flag, simplified strong silhouette`

Negative prompt:
`large building, blur, scenic background, text, realistic fort`

PixelLab notes:
One of the easiest icons to over-detail. Keep it compact.

### node_crossing.png
Size: `16x16`
Path: `assets/images/map/nodes/`

Prompt:
`clean retro 16-bit inspired pixel art map node icon, 16x16 transparent background, wavy blue river line with a small crossing arrow, simple and readable, travel hazard marker`

Negative prompt:
`large bridge scene, blur, text, photoreal water`

PixelLab notes:
Prioritize icon legibility over realism.

### node_mountain.png
Size: `16x16`
Path: `assets/images/map/nodes/`

Prompt:
`clean retro 16-bit inspired pixel art map node icon, 16x16 transparent background, small jagged mountain silhouette, stone mid color, simple readable terrain marker`

Negative prompt:
`complex scene, blur, trees, text, realistic mountain painting`

PixelLab notes:
Keep the mountain shape bold and centered.

### node_town.png
Size: `16x16`
Path: `assets/images/map/nodes/`

Prompt:
`clean retro 16-bit inspired pixel art map node icon, 16x16 transparent background, tiny building with chimney, wood warm palette, simple small town marker, strong silhouette`

Negative prompt:
`large street scene, blur, text, modern house, extra background`

PixelLab notes:
Match the visual weight of the other map nodes.

## Icons — Inventory

### icon_food.png
Size: `16x16`
Path: `assets/images/icons/inventory/`

Prompt:
`clean retro 16-bit inspired pixel art inventory icon, 16x16 transparent background, smoked or dried meat bundle, earthy browns, small highlight, bold silhouette, readable at tiny size`

Negative prompt:
`plate of food, modern packaging, blur, text, realistic texture`

PixelLab notes:
Aim for silhouette first, texture second.

### icon_water.png
Size: `16x16`
Path: `assets/images/icons/inventory/`

Prompt:
`clean retro 16-bit inspired pixel art inventory icon, 16x16 transparent background, small wooden barrel with a slight blue tint and a tiny water droplet mark, readable tiny sprite`

Negative prompt:
`glass bottle, blur, text, realistic barrel shading, large splash`

PixelLab notes:
Keep it distinct from medicine.

### icon_medicine.png
Size: `16x16`
Path: `assets/images/icons/inventory/`

Prompt:
`clean retro 16-bit inspired pixel art inventory icon, 16x16 transparent background, small brown medicine bottle with cork top, tiny cream label or white cross, frontier remedy item, readable silhouette`

Negative prompt:
`modern pill bottle, syringe, blur, text, transparent glass realism`

PixelLab notes:
The cork should help separate it from water and ammo.

### icon_ammunition.png
Size: `16x16`
Path: `assets/images/icons/inventory/`

Prompt:
`clean retro 16-bit inspired pixel art inventory icon, 16x16 transparent background, three small bullets stacked or a compact powder horn, dark metal grey and wood accents, readable small silhouette`

Negative prompt:
`modern assault ammo box, gun, blur, text, photoreal metal`

PixelLab notes:
Prefer the clearer silhouette between bullets and powder horn after generation.

### icon_clothing.png
Size: `16x16`
Path: `assets/images/icons/inventory/`

Prompt:
`clean retro 16-bit inspired pixel art inventory icon, 16x16 transparent background, folded coat or shirt, warm brown grey cloth, simple readable shape`

Negative prompt:
`full character, blur, text, modern tshirt graphic, realistic fabric folds`

PixelLab notes:
Avoid tiny decorative details that will disappear.

### icon_wagon_parts.png
Size: `16x16`
Path: `assets/images/icons/inventory/`

Prompt:
`clean retro 16-bit inspired pixel art inventory icon, 16x16 transparent background, spare wagon wheel side view, wood warm spokes, compact readable silhouette`

Negative prompt:
`entire wagon, blur, text, realistic wheel texture`

PixelLab notes:
This should visually echo the wagon sprite.

### icon_money.png
Size: `16x16`
Path: `assets/images/icons/inventory/`

Prompt:
`clean retro 16-bit inspired pixel art inventory icon, 16x16 transparent background, small coin stack, gold with stone dark shadow edge, frontier currency icon, bright and readable`

Negative prompt:
`paper money, treasure chest, blur, text, photoreal coin reflections`

PixelLab notes:
Make this one slightly brighter than neighboring inventory icons.

### icon_oxen.png
Size: `16x16`
Path: `assets/images/icons/inventory/`

Prompt:
`clean retro 16-bit inspired pixel art inventory icon, 16x16 transparent background, single ox head in side view, brown tones, simple horn shape, bold silhouette`

Negative prompt:
`full animal body, blur, text, realistic fur, cow face front view`

PixelLab notes:
This should visually rhyme with the oxen sprites.

### icon_tools.png
Size: `16x16`
Path: `assets/images/icons/inventory/`

Prompt:
`clean retro 16-bit inspired pixel art inventory icon, 16x16 transparent background, hammer or axe, stone mid metal head and wood warm handle, simple utility icon, readable silhouette`

Negative prompt:
`toolbox, modern wrench set, blur, text, realism`

PixelLab notes:
Pick whichever tool gives the cleaner 16x16 silhouette.

## Icons — Status

### status_healthy.png
Size: `16x16`
Path: `assets/images/icons/status/`

Prompt:
`clean retro 16-bit inspired pixel art status icon, 16x16 transparent background, solid heart icon, green good color, simple centered silhouette`

Negative prompt:
`realistic anatomical heart, blur, text, extra decoration`

PixelLab notes:
Keep the shape clean and familiar.

### status_hungry.png
Size: `16x16`
Path: `assets/images/icons/status/`

Prompt:
`clean retro 16-bit inspired pixel art status icon, 16x16 transparent background, empty bowl with small fork, yellow alert tones, readable hunger symbol`

Negative prompt:
`full meal, blur, text, oversized utensils, realism`

PixelLab notes:
The bowl silhouette should dominate.

### status_sick.png
Size: `16x16`
Path: `assets/images/icons/status/`

Prompt:
`clean retro 16-bit inspired pixel art status icon, 16x16 transparent background, small skull or ill green face, green mid and grey muted palette, readable sickness symbol`

Negative prompt:
`gore, horror realism, blur, text, giant face detail`

PixelLab notes:
Use whichever concept reads better at 16x16.

### status_injured.png
Size: `16x16`
Path: `assets/images/icons/status/`

Prompt:
`clean retro 16-bit inspired pixel art status icon, 16x16 transparent background, cream bandage with red danger cross, centered readable injury symbol`

Negative prompt:
`blood, gore, blur, text, realistic bandage texture`

PixelLab notes:
Keep the cross bold and centered.

### status_exhausted.png
Size: `16x16`
Path: `assets/images/icons/status/`

Prompt:
`clean retro 16-bit inspired pixel art status icon, 16x16 transparent background, small drooping eye or pixel zzz symbol, grey muted palette, clear exhaustion status icon`

Negative prompt:
`large text block, blur, realistic eyelid painting, extra decoration`

PixelLab notes:
Pick the version that stays clearest after downscaling.

### status_dead.png
Size: `16x16`
Path: `assets/images/icons/status/`

Prompt:
`clean retro 16-bit inspired pixel art status icon, 16x16 transparent background, simple tombstone silhouette, stone mid color, centered and readable`

Negative prompt:
`graveyard scene, blur, text, skull pile, realism`

PixelLab notes:
Understated and clear is better than dramatic.

### status_morale_high.png
Size: `16x16`
Path: `assets/images/icons/status/`

Prompt:
`clean retro 16-bit inspired pixel art status icon, 16x16 transparent background, raised fist or smiling face, gold palette, positive morale symbol, simple and energetic`

Negative prompt:
`complex character portrait, blur, text, realism`

PixelLab notes:
Use the clearer silhouette between fist and face.

### status_morale_low.png
Size: `16x16`
Path: `assets/images/icons/status/`

Prompt:
`clean retro 16-bit inspired pixel art status icon, 16x16 transparent background, frowning face, grey muted tones, low morale symbol, readable at tiny size`

Negative prompt:
`complex portrait, blur, text, realism, angry screaming face`

PixelLab notes:
Keep it subdued rather than theatrical.

### status_morale_critical.png
Size: `16x16`
Path: `assets/images/icons/status/`

Prompt:
`clean retro 16-bit inspired pixel art status icon, 16x16 transparent background, cracked heart or angry face, red danger palette, critical morale warning symbol, strong silhouette`

Negative prompt:
`gore, blur, text, photoreal face, oversized effects`

PixelLab notes:
Choose the icon that contrasts best with `status_morale_low`.

## Event Art

### event_storm.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, dark storm over the trail, churning sky deep clouds, lightning bolt, heavy rain streaks, threatening mood, stone dark ground, water light rain highlights, readable composition with room for overlay text`

Negative prompt:
`sunny weather, photoreal clouds, blur, text labels, modern road`

PixelLab notes:
These event images sit behind text, so keep the center readable.

### event_illness.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, dim wagon interior, warm lantern glow, one party member shape lying under a blanket, intimate somber mood, wood interior, soft but crisp pixel lighting, readable background for event text`

Negative prompt:
`hospital room, gore, blur, text, modern bed, photoreal interior`

PixelLab notes:
Use contrast carefully so the lantern glow carries the scene.

### event_broken_wheel.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, roadside wagon tilted with a cracked wheel, tools scattered nearby, dusty trail, travel interruption, clear visual focus on the damage`

Negative prompt:
`full destruction, fire, blur, text, modern tools, photoreal detail`

PixelLab notes:
This should feel inconvenient, not apocalyptic.

### event_river_flood.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, river swollen above its banks, muddy rushing water, floating debris, near crossing panic, dangerous frontier flood, dynamic but readable composition`

Negative prompt:
`calm river, blur, text, bridge traffic, photoreal water`

PixelLab notes:
Push movement with foam and debris, not with visual noise.

### event_good_hunting.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, open sunny plains, deer or bison silhouettes in the middle distance, bright blue sky, green grass, hopeful resource opportunity, clear horizon`

Negative prompt:
`blood, hunting gore, blur, text, dense forest, photoreal animals`

PixelLab notes:
Keep the tone optimistic and open.

### event_harsh_weather.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, harsh weather whiteout or dust storm, barely visible wagon outline, near white or tan haze, dangerous low visibility, simple shapes emerging through the storm`

Negative prompt:
`clear sky, blur that destroys all forms, text, photoreal particles, modern vehicle`

PixelLab notes:
The challenge is visibility without losing the wagon silhouette completely.

### event_lost_trail.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, dense forest at dusk, forked path with no clear marker, shafts of dim light through trees, uncertain mood, trail confusion scene`

Negative prompt:
`bright noon scene, clear signage, blur, text, photoreal woods`

PixelLab notes:
Make the fork readable from the first glance.

### event_friendly_encounter.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, peaceful meeting on the trail, two small groups exchanging goods, warm midday light, calm open setting, helpful encounter mood`

Negative prompt:
`fight, blur, text, modern marketplace, overcrowded detail`

PixelLab notes:
This should feel welcoming and balanced.

### event_theft.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, night on the trail, shadowy silhouettes on a ridge above camp, small campfire visible below, tense and ominous, dark sky, hidden threat`

Negative prompt:
`direct battle, gore, blur, text, bright daylight, photoreal stealth scene`

PixelLab notes:
Keep the silhouettes suggestive rather than explicit.

### event_good_rest.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, peaceful campfire scene at night, clear starry sky, wagon resting nearby, calm warm glow, safe resting mood, simple readable silhouettes`

Negative prompt:
`storm, blur, text, crowded campsite, photoreal stars`

PixelLab notes:
The emotional job here is relief.

### event_find_supplies.png
PixelLab generation size: `192x192`
Final export size: `160x96`
Path: `assets/images/events/`

Prompt:
`retro 16-bit inspired pixel art event card scene, 160x96, abandoned supply cache by the trail, crates and barrels half buried or stacked, lucky discovery energy, warm daylight, frontier resource find`

Negative prompt:
`modern supply drop, blur, text, huge treasure room, photoreal crates`

PixelLab notes:
Keep the cache readable without overfilling the small scene.

## Store

### store_background.png
PixelLab generation size: `320x320`
Final export size: `320x160`
Path: `assets/images/store/`

Prompt:
`retro 16-bit inspired pixel art store background, 320x160 scene, frontier general store interior, wood plank walls, shelves with barrels boxes and hanging goods, wooden counter in front, warm lantern light, cozy rustic interior, readable broad shapes for a game shop screen`

Negative prompt:
`modern grocery store, blur, text signs, photoreal shelves, clutter that hides the layout`

PixelLab notes:
Keep the middle and lower areas clean enough for UI and items overlays.

### store_counter.png
PixelLab generation size: `192x192`
Final export size: `160x32`
Path: `assets/images/store/`

Prompt:
`retro 16-bit inspired pixel art store counter strip, 160x32, wooden countertop surface, visible plank grain, warm browns, simple overlay element, side-on view, readable repeating wood texture`

Negative prompt:
`full store room, blur, text, perspective angle, objects sitting on top`

PixelLab notes:
Keep it simple so it can composite cleanly.

## UI — Panels and Chrome

### panel_frame_corner_tl.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui tile, 8x8 transparent background, top left corner of a 9-slice panel frame, wood and rope texture, ui border color, crisp tiny tile`

Negative prompt:
`large panel, blur, text, modern glossy ui`

PixelLab notes:
Generate tiny UI tiles very cleanly; plan on manual pixel cleanup.

### panel_frame_corner_tr.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui tile, 8x8 transparent background, top right corner of a 9-slice panel frame, wood and rope texture, mirror partner to top left corner`

Negative prompt:
`large panel, blur, text, glossy effects`

PixelLab notes:
If PixelLab struggles, mirror the top-left tile manually after generation.

### panel_frame_corner_bl.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui tile, 8x8 transparent background, bottom left corner of a 9-slice panel frame, wood and rope texture, crisp tiny corner`

Negative prompt:
`large panel, blur, text, glossy ui`

PixelLab notes:
Match the visual weight of the top corners.

### panel_frame_corner_br.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui tile, 8x8 transparent background, bottom right corner of a 9-slice panel frame, wood and rope texture, crisp tiny corner`

Negative prompt:
`large panel, blur, text, glossy ui`

PixelLab notes:
If symmetry is cleaner, mirror from bottom-left after generation.

### panel_frame_edge_top.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui tile, 8x8 transparent background, tileable top panel edge, rope or wood beam texture, horizontal repeatable border segment`

Negative prompt:
`non tileable art, blur, text, large decorative object`

PixelLab notes:
This must tile horizontally without obvious seams.

### panel_frame_edge_bottom.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui tile, 8x8 transparent background, tileable bottom panel edge, rope or wood beam texture, horizontal repeatable border segment`

Negative prompt:
`non tileable art, blur, text, glossy ui`

PixelLab notes:
Keep it consistent with the top edge.

### panel_frame_edge_left.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui tile, 8x8 transparent background, tileable left panel edge, rope or wood beam texture, vertical repeatable border segment`

Negative prompt:
`non tileable art, blur, text, large ornament`

PixelLab notes:
This must tile vertically.

### panel_frame_edge_right.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui tile, 8x8 transparent background, tileable right panel edge, rope or wood beam texture, vertical repeatable border segment`

Negative prompt:
`non tileable art, blur, text, glossy ui`

PixelLab notes:
Keep it as the right-side partner to the left edge.

### panel_fill_dark.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui fill tile, 8x8, dark panel fill using ui dark color, subtle grain, tileable texture, simple interior panel background`

Negative prompt:
`ornate decoration, blur, text, gradients, strong directional lighting`

PixelLab notes:
This should disappear behind content, not attract attention.

### panel_fill_parchment.png
Size: `8x8`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui fill tile, 8x8, parchment panel fill, aged tan paper texture, subtle grain, tileable, simple readable interior background`

Negative prompt:
`heavy stains, blur, text, photo texture, strong shadow`

PixelLab notes:
Keep the pattern low contrast for readability.

### button_normal.png
PixelLab generation size: `128x128`
Final export size: `80x16`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui button, 80x16 transparent background, stone mid button face, stone light highlight on top and left edges, stone dark shadow on bottom and right edges, classic raised game button, no label text`

Negative prompt:
`glossy modern button, blur, text, rounded modern app style`

PixelLab notes:
This is a reusable base button, not a specific menu label.

### button_pressed.png
PixelLab generation size: `128x128`
Final export size: `80x16`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui button, 80x16 transparent background, pressed button state, slightly darker stone fill, inverted highlight and shadow so the face looks pushed in, no text`

Negative prompt:
`modern glossy button, blur, label text, glowing effects`

PixelLab notes:
Keep it clearly related to `button_normal`.

### button_disabled.png
PixelLab generation size: `128x128`
Final export size: `80x16`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui button, 80x16 transparent background, disabled state, grey muted fill, minimal contrast, no highlight sparkle, no text, readable as inactive`

Negative prompt:
`glow, bright colors, blur, label text, glossy ui`

PixelLab notes:
This should look visibly unavailable at a glance.

### divider_horizontal.png
PixelLab generation size: `320x320`
Final export size: `320x4`
Path: `assets/images/ui/`

Prompt:
`clean retro 16-bit inspired pixel art ui divider, 320x4 transparent background, thin horizontal rope or wood grain line, decorative separator, simple repeated texture`

Negative prompt:
`thick banner, blur, text, ornate frame, glossy ui`

PixelLab notes:
A simple repeating motif is better than a highly detailed divider.

### scroll_bg.png
PixelLab generation size: `192x192`
Final export size: `160x80`
Path: `assets/images/ui/`

Prompt:
`retro 16-bit inspired pixel art parchment scroll panel, 160x80, aged scroll texture, slightly rolled top and bottom edges, parchment and parchment dim tones, readable background for text, centered composition`

Negative prompt:
`full manuscript with writing, blur, ornate fantasy scroll, photoreal paper`

PixelLab notes:
Leave the inner area calm enough for text readability.

## UI — HUD

### hud_bar_track.png
PixelLab generation size: `64x64`
Final export size: `64x8`
Path: `assets/images/ui/hud/`

Prompt:
`clean retro 16-bit inspired pixel art hud bar track, 64x8 transparent background, ui dark outer track, subtle inner shadow edge, empty bar frame, clean tileable horizontal look`

Negative prompt:
`filled bar, blur, text, modern glossy meter`

PixelLab notes:
This should pair with all fill assets.

### hud_bar_fill_health.png
PixelLab generation size: `64x64`
Final export size: `64x8`
Path: `assets/images/ui/hud/`

Prompt:
`clean retro 16-bit inspired pixel art hud bar fill, 64x8 transparent background, red bright horizontal fill texture, tileable on x axis, simple subtle pixel shading`

Negative prompt:
`track border, blur, text, gradients, glossy shine`

PixelLab notes:
Keep it simple since code will mask the width.

### hud_bar_fill_food.png
PixelLab generation size: `64x64`
Final export size: `64x8`
Path: `assets/images/ui/hud/`

Prompt:
`clean retro 16-bit inspired pixel art hud bar fill, 64x8 transparent background, dirt light horizontal fill texture, tileable on x axis, simple subtle pixel shading`

Negative prompt:
`track border, blur, text, gradients, glossy effects`

PixelLab notes:
Match the health bar texture style.

### hud_bar_fill_water.png
PixelLab generation size: `64x64`
Final export size: `64x8`
Path: `assets/images/ui/hud/`

Prompt:
`clean retro 16-bit inspired pixel art hud bar fill, 64x8 transparent background, water light horizontal fill texture, tileable on x axis, subtle pixel sheen`

Negative prompt:
`track border, blur, text, wave scene, heavy gradients`

PixelLab notes:
Keep the pattern restrained so it masks cleanly.

### hud_bar_fill_money.png
PixelLab generation size: `64x64`
Final export size: `64x8`
Path: `assets/images/ui/hud/`

Prompt:
`clean retro 16-bit inspired pixel art hud bar fill, 64x8 transparent background, gold horizontal fill texture, tileable on x axis, simple bright resource fill`

Negative prompt:
`track border, blur, text, coin illustrations, glossy ui`

PixelLab notes:
Brightness is enough; avoid tiny coin details.

### hud_bar_fill_morale.png
PixelLab generation size: `64x64`
Final export size: `64x8`
Path: `assets/images/ui/hud/`

Prompt:
`clean retro 16-bit inspired pixel art hud bar fill, 64x8 transparent background, yellow alert morale fill texture, tileable on x axis, simple energetic fill`

Negative prompt:
`track border, blur, text, smiley faces, gradients`

PixelLab notes:
Keep it visually distinct from food and money.

### hud_bar_fill_wagon.png
PixelLab generation size: `64x64`
Final export size: `64x8`
Path: `assets/images/ui/hud/`

Prompt:
`clean retro 16-bit inspired pixel art hud bar fill, 64x8 transparent background, wood warm wagon condition fill texture, tileable on x axis, subtle wood-toned resource fill`

Negative prompt:
`track border, blur, text, literal wagon illustration, glossy ui`

PixelLab notes:
Do not over-literalize the wagon theme.

### hud_portrait_frame.png
Size: `24x24`
Path: `assets/images/ui/hud/`

Prompt:
`clean retro 16-bit inspired pixel art hud portrait frame, 24x24 transparent background, small square avatar border, wood and rope style matching panel frame assets, open center for character portrait, readable at tiny size`

Negative prompt:
`full portrait, blur, text, glossy modern frame`

PixelLab notes:
This should visually match the panel frame kit.

## Weather Overlays

### weather_rain.png
Size: `64x64`
Path: `assets/images/weather/`

Prompt:
`retro 16-bit inspired pixel art weather overlay tile, 64x64 transparent background, diagonal rain streaks from upper left to lower right, water light color, sparse density, semi transparent feel, tileable on both axes`

Negative prompt:
`storm background scene, blur, text, thick fog, realistic droplets`

PixelLab notes:
This is an overlay tile, not a full scene. Expect manual alpha cleanup.

### weather_heavy_rain.png
Size: `64x64`
Path: `assets/images/weather/`

Prompt:
`retro 16-bit inspired pixel art weather overlay tile, 64x64 transparent background, denser diagonal rain streaks, slightly wider lines, water mid color, heavier rainfall, tileable on both axes`

Negative prompt:
`background scenery, blur, text, giant splashes, photoreal rain`

PixelLab notes:
Keep the direction consistent with `weather_rain`.

### weather_snow.png
Size: `64x64`
Path: `assets/images/weather/`

Prompt:
`retro 16-bit inspired pixel art weather overlay tile, 64x64 transparent background, scattered small round snow dots with slight size variation, white and sky pale colors, light semi transparent feel, tileable on both axes`

Negative prompt:
`winter landscape scene, blur, text, giant snowflakes, photoreal snow`

PixelLab notes:
Use sparse randomness but preserve tileability.

### weather_dust.png
Size: `64x64`
Path: `assets/images/weather/`

Prompt:
`retro 16-bit inspired pixel art weather overlay tile, 64x64 transparent background, horizontal dust haze bands, dirt pale color, dry plains feel, semi transparent, tileable on both axes`

Negative prompt:
`sandstorm scene with background, blur, text, giant debris`

PixelLab notes:
Keep contrast low so the overlay layers softly over scenes.

### weather_fog.png
Size: `64x64`
Path: `assets/images/weather/`

Prompt:
`retro 16-bit inspired pixel art weather overlay tile, 64x64 transparent background, dense soft haze, sky pale color, slight density variation, flat fog overlay, tileable on both axes`

Negative prompt:
`cloud scene, blur that erases all form, text, realistic vapor photography`

PixelLab notes:
This should be the softest and least directional weather tile.

## Full Screens

### screen_title.png
PixelLab generation size: `576x576`
Final export size: `320x568`
Path: `assets/images/screens/`

Prompt:
`retro 16-bit inspired pixel art title screen, 320x568 portrait scene, dramatic wagon silhouette on a trail at sunset, rich warm sky, cinematic but readable composition, large open space in the top third for a game logo, strong horizon, frontier adventure mood`

Negative prompt:
`text logo included, modern ui, blur, photoreal sky, crowded composition, modern road`

PixelLab notes:
Leave negative space at the top for the title treatment.

### screen_victory.png
PixelLab generation size: `576x576`
Final export size: `320x568`
Path: `assets/images/screens/`

Prompt:
`retro 16-bit inspired pixel art victory screen, 320x568 portrait scene, wagon arriving in Willamette Valley, green rolling hills, river, farmland, warm golden sky, party figures celebrating in the foreground, triumphant and hopeful, lush final destination`

Negative prompt:
`text, blur, dark storm, barren land, photoreal farming equipment`

PixelLab notes:
This should be the emotional release image for the campaign.

### screen_gameover.png
PixelLab generation size: `576x576`
Final export size: `320x568`
Path: `assets/images/screens/`

Prompt:
`retro 16-bit inspired pixel art game over screen, 320x568 portrait scene, desolate trail, single tombstone in the foreground, abandoned wagon in the distance, cool blue grey palette, somber empty atmosphere, sparse and quiet composition`

Negative prompt:
`gore, text, blur, dramatic battle, bright happy colors, photoreal realism`

PixelLab notes:
Keep the composition simple and emotionally heavy.

### screen_loading.png
PixelLab generation size: `576x576`
Final export size: `320x568`
Path: `assets/images/screens/`

Prompt:
`retro 16-bit inspired pixel art loading screen, 320x568 portrait scene, simple trail composition with wagon wheel motion implication, minimal scene design, readable center area, frontier travel mood, restrained detail suitable for a loading screen`

Negative prompt:
`text, blur, full cinematic splash, busy composition, modern ui`

PixelLab notes:
Keep this intentionally simpler than the title and victory screens.
