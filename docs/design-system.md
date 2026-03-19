# Design System — vibes-oregon-trail

Visual style guide for pixel art assets. All assets target a **16-bit homage** aesthetic (late 80s/early 90s SNES/Genesis era). This is not a strict recreation — it's an aesthetic reference point with modern mobile readability.

---

## Orientation

### Lock to Portrait

This game is **portrait-only**. Lock orientation in Expo config (`orientation: "portrait"` in `app.json`).

**Why portrait:**
- The Oregon Trail route reads naturally top-to-bottom on a tall screen
- HUD panels stack below scene art cleanly in portrait
- One-handed mobile play is portrait by default
- Landmark scenes work as full-width horizontal banners within a portrait layout
- All assets are designed for one canvas shape — no duplicates for landscape

**Landscape is not supported in v1.** If it's added later, it requires a separate layout pass and potentially separate scene art. Don't design assets with landscape in mind now.

### Safe Area

Modern phones have notches, dynamic islands, and home indicator bars. All interactive elements and readable text must stay within the **safe area inset**.

Design rule: keep a **16px (1 tile) minimum margin** from all screen edges for any tappable UI or critical text. The engine handles safe area insets — this is just an art awareness note.

---

## Display Strategy

### The Core Approach

Pixel art looks bad when scaled with bilinear filtering. It must scale with **nearest-neighbor interpolation only**, at **integer multiples**.

This game renders to a **logical pixel art canvas**, then scales up to fill the device screen. Think of it like rendering to a tiny retro screen and blowing it up cleanly.

### Base Tile Unit

**1 tile = 16px**

All art should be designed on a 16px grid. Sprites, icons, panels — everything snaps to multiples of 16.

### Logical Canvas Size

**320 × 568 logical pixels**

This is the art canvas. It maps to the game world. At 3× scale it fills most modern phones without letterboxing.

| Scale | Resolution      | Target Devices                            |
|-------|-----------------|-------------------------------------------|
| 1×    | 320 × 568       | Reference / low-DPI fallback              |
| 2×    | 640 × 1136      | iPad non-retina, older Android mdpi/hdpi  |
| 3×    | 960 × 1704      | iPhone (all modern), Android xhdpi+       |

### Export Format

Export all assets at **3× base size** unless noted. For React Native / Expo:

```
icon_food.png       ← 1× (base size)
icon_food@2x.png    ← 2× (2× base)
icon_food@3x.png    ← 3× (3× base)
```

Expo automatically selects the right file based on screen density. Always provide all three.

For **full-screen backgrounds and landmark scenes**, 3× only is acceptable. They don't need 1× or 2× variants — scale down in code if needed.

### Pixel Art Scaling Rule

> When exporting multi-scale assets from PixelLab, use **integer scaling only** (1×, 2×, 3×). Never use fractional scales. Never use bilinear or smooth scaling. Nearest-neighbor only.

---

## Color Palette

Limit to **32 colors across the entire game**. Consistency matters more than variety. Sprites and UI should pull from the same master palette.

### Master Palette

#### Sky & Atmosphere
| Name          | Hex       | Use                               |
|---------------|-----------|-----------------------------------|
| Sky Deep      | `#3A5F8A` | Night sky, deep water             |
| Sky Mid       | `#5B8DD9` | Daytime sky                       |
| Sky Light     | `#9BB8E8` | Upper sky, highlights             |
| Sky Pale      | `#D4E8FF` | Horizon, haze                     |

#### Earth & Terrain
| Name          | Hex       | Use                               |
|---------------|-----------|-----------------------------------|
| Dirt Dark     | `#5C3D1E` | Shadows, deep ground              |
| Dirt Mid      | `#8B5E2A` | Trail, terrain base               |
| Dirt Light    | `#C4A46B` | Sunlit ground, sand               |
| Dirt Pale     | `#E8D4A0` | Highlights, dry grass             |

#### Vegetation
| Name          | Hex       | Use                               |
|---------------|-----------|-----------------------------------|
| Green Dark    | `#2D5A27` | Shadows, dense trees              |
| Green Mid     | `#4A7A3A` | Grass, foliage base               |
| Green Light   | `#6AAF52` | Lit foliage, plains               |
| Green Pale    | `#9BD67A` | Highlights, fresh growth          |

#### Rock & Wood
| Name          | Hex       | Use                               |
|---------------|-----------|-----------------------------------|
| Stone Dark    | `#3C2E24` | Rock shadows                      |
| Stone Mid     | `#5A4A3C` | Rock, dry timber                  |
| Stone Light   | `#847060` | Lit rock, weathered wood          |
| Wood Warm     | `#A0622A` | Wagon, fences, buildings          |
| Wood Light    | `#C88040` | Lit wood surfaces                 |

#### Water
| Name          | Hex       | Use                               |
|---------------|-----------|-----------------------------------|
| Water Dark    | `#1E4E6E` | Deep water, shadow                |
| Water Mid     | `#2D6B9E` | River base                        |
| Water Light   | `#4A9BC5` | Lit water, shallow areas          |
| Water Foam    | `#A8D4E8` | Foam, rapids, reflection          |

#### UI & Interface
| Name          | Hex       | Use                               |
|---------------|-----------|-----------------------------------|
| UI Dark       | `#1A1A2E` | Panel backgrounds, dark UI        |
| UI Mid        | `#2D2D44` | Secondary panels, borders         |
| UI Border     | `#4A3C28` | Panel frames, wood trim           |
| Parchment     | `#E8D5A3` | Text backgrounds, scroll UI       |
| Parchment Dim | `#C8B47A` | Dimmed parchment, shadows         |
| Cream         | `#FFF5DC` | Primary text on dark backgrounds  |

#### Status & Accent
| Name          | Hex       | Use                               |
|---------------|-----------|-----------------------------------|
| Red Danger    | `#D43030` | Health loss, danger, death        |
| Red Bright    | `#F05050` | HP bar, injury icon               |
| Yellow Alert  | `#F5A623` | Warning, hunger, morale mid       |
| Gold          | `#F5D020` | Money, treasure, XP               |
| Green Good    | `#3DAA5A` | Health full, positive status      |
| Grey Muted    | `#787878` | Disabled, dead, exhausted         |

---

## Typography

### Primary Font: Press Start 2P

Google Fonts. Free. The canonical retro game pixel font.

```
https://fonts.google.com/specimen/Press+Start+2P
```

This font is **8px base height**. At 3× scale it renders at 24px physical pixels — crisp and readable on modern phones.

### Size Scale

All sizes are in **logical canvas pixels** (before device scaling):

| Role             | Size  | Use                                      |
|------------------|-------|------------------------------------------|
| Heading          | 16px  | Screen titles, landmark names            |
| Body             | 8px   | Descriptions, event text, store items    |
| Label            | 8px   | HUD labels, button text                  |
| Micro            | 6px   | Quantity numbers, small overlays         |

> Note: Press Start 2P at 8px is already small. Never go below 8px at canvas resolution. On-screen text must be readable at arm's length on a phone.

### Line Height

2× font size. For 8px text, 16px line height. Press Start 2P needs room.

### Text Rendering

Use **nearest-neighbor / no anti-aliasing** on font rendering where possible. On React Native, this typically means using the font as-is and avoiding text shadow effects that blur pixel boundaries.

---

## Sprite Standards

All sprites are built on a **16px tile grid**. Sizes below are **base (1×) canvas dimensions**.

### Characters

| Type              | Base Size  | Notes                            |
|-------------------|------------|----------------------------------|
| Party member      | 16 × 32    | 1 tile wide, 2 tiles tall        |
| NPC / Shopkeeper  | 24 × 40    | Slightly larger for readability  |

### Wagon & Animals

| Type              | Base Size  | Notes                            |
|-------------------|------------|----------------------------------|
| Wagon (side view) | 64 × 40    | 4 tiles wide, 2.5 tiles tall     |
| Oxen pair         | 48 × 24    | 3 tiles wide, 1.5 tiles tall     |

### Map Nodes

| Type              | Base Size  | Notes                            |
|-------------------|------------|----------------------------------|
| Map node icon     | 16 × 16    | 1 tile, all variants             |

### Icons

| Type              | Base Size  | Notes                            |
|-------------------|------------|----------------------------------|
| Inventory icon    | 16 × 16    | 1 tile                           |
| Status icon       | 16 × 16    | 1 tile                           |

### Scenes / Backgrounds

| Type              | Base Size  | Notes                            |
|-------------------|------------|----------------------------------|
| Landmark scene    | 320 × 128  | Full canvas width, ~8 tiles tall |
| Event card art    | 160 × 96   | Half-width, 6 tiles tall         |
| Store background  | 320 × 160  | Full canvas width                |
| Full screen       | 320 × 568  | Full canvas, victory/gameover    |

### HUD Elements

| Type              | Base Size  | Notes                            |
|-------------------|------------|----------------------------------|
| Resource bar      | 64 × 8     | 4 tiles wide, half tile tall     |
| Panel frame tile  | 8 × 8      | 9-slice, borders + corners       |
| Button            | 80 × 16    | 5 tiles wide, 1 tile tall        |

---

## UI Component Rules

### Panels

- All panels use a **9-slice border** system (corner tiles + edge tiles + center fill)
- Border tile is 8×8px
- Panel background: `UI Dark` or `Parchment` depending on context
- Border color: `UI Border` (wood frame look)

### Buttons

- Normal state: `Stone Mid` fill, `Stone Light` top/left highlight, `Stone Dark` bottom/right shadow
- Pressed state: invert the highlights (feels like the button depresses)
- Label text in `Cream`

### HUD Resource Bars

- Outer track: `UI Dark`
- Fill color varies by resource type:
  - Health: `Red Bright`
  - Food: `Dirt Light`
  - Water: `Water Light`
  - Money: `Gold`
  - Wagon: `Wood Warm`
  - Morale: `Yellow Alert` → `Green Good` depending on level

### Status Indicators

- Healthy: `Green Good`
- Warning / degraded: `Yellow Alert`
- Critical / danger: `Red Danger`
- Dead / disabled: `Grey Muted`

---

## Animation Guidelines

For PixelLab, produce **individual frames** as separate assets. The game engine handles sequencing.

### Frame Rates (at canvas clock)

| Animation Type    | FPS  | Notes                                  |
|-------------------|------|----------------------------------------|
| Idle (breathing)  | 4    | Subtle, slow                           |
| Walking / travel  | 8    | Smooth enough to read motion           |
| Event / action    | 8–12 | More expressive                        |
| UI flash / alert  | 4–6  | Not too distracting                    |

### Frame Naming

```
wagon_travel_f01.png
wagon_travel_f02.png
wagon_travel_f03.png
wagon_travel_f04.png
```

---

## File Format

| Use Case                | Format  | Notes                              |
|-------------------------|---------|------------------------------------|
| Sprites with transparency | PNG   | Always                             |
| Full-screen backgrounds | PNG     | No JPEG — compression artifacts    |
| UI elements             | PNG     | Transparency required              |

No JPEG. No WebP (unless specifically needed for a background). PNG throughout.

---

## Folder Structure

```
assets/
├── images/
│   ├── sprites/
│   │   ├── wagon/
│   │   ├── party/
│   │   ├── oxen/
│   │   └── npc/
│   ├── landmarks/
│   ├── map/
│   ├── icons/
│   │   ├── inventory/
│   │   └── status/
│   ├── events/
│   ├── store/
│   ├── ui/
│   │   └── hud/
│   ├── weather/
│   └── screens/
├── fonts/
└── audio/
```

---

## PixelLab Workflow Notes

1. Create at **base (1×) size**
2. Export at 1×, 2×, 3× using nearest-neighbor scaling
3. Name files with `@2x` and `@3x` suffixes
4. Place in the correct `assets/images/` subfolder
5. Mark the asset as done in `docs/asset-list.md`

When using PixelLab's color picker, import the master palette above as a custom palette and **lock to it**. Consistency across sessions is the goal.
