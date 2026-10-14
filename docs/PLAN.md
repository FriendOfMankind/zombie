# Surrealist FPS: plan skeleton

Status: **skeleton**. Anything marked `TBD` hasn't been decided. Anything marked `?` is a guess waiting on Colin.

## The one-line pitch (draft)

A fast, ugly-beautiful first-person shooter where **movement is the main verb**, the world is built from handmade, gross textures (clay, scans, blown-out colour), and the **HUD itself is part of the hallucination**.

Working title: `zombie` (the repo name) `?`

## What the reference clips are actually giving us

| Ref | What's on screen | Steal this | Don't steal this |
|---|---|---|---|
| 1. Green cube maze, orange fanged blobs | Flat-shaded voxel world, enemies in one loud colour, 11-slot weapon bar with ammo counts, DPS meter, target label ("Demon: 1") | **Readability.** Enemies pop off a calm world. A big arsenal you scroll through. Numbers that go up. | Flat green everywhere gets boring fast |
| 2–3. Cruelty Squad, plus split-screen feeds (Gerald Ford speech, Uma Musume race) | Garish organic HUD frame, colour palettes cranked until they hurt, spiky "DEMON" decals, low-poly with cheap textures | **Hostile aesthetic on purpose.** The UI frame is meat. Colour is a weapon. | Its difficulty and opacity: Cruelty Squad earns them with a deep immersive-sim loop underneath. We don't have that yet. |
| 4–5. Clay world, "864 × 12 SURFING + WALL + FREE FALLING + SURFING" | Plasticine/clay textures on everything, green clay zombie hands as the viewmodel, portrait medallions in the corners, trick-combo score with multiplier | **Movement tricks chain into a style score** (Tony Hawk logic in an FPS). Handmade physical textures. Zombie hands. | — |

Open question: are the split-screen feeds in 2–3 **part of the inspiration** (a HUD that fights you for attention) or just how the clip was posted? See Q4.

## Pillars (draft, max 4)

1. **Movement is the verb.** Surfing ramps, wall-runs, free-fall, slides. Shooting is how you *spend* momentum, not the point.
2. **Style is the score.** Every trick names itself on screen and multiplies. Standing still kills the combo.
3. **Handmade gross.** Real-world textures (clay, food, skin, carpet, scans) on cheap geometry. Low poly, high texture-weirdness.
4. **The interface is haunted.** HUD frame, corner portraits and side feeds react, lie, distract and mutate.

If a feature doesn't serve one of these, it's cut.

## Core loop

```
enter arena → chain movement (score ×) → kill with arsenal (score +) → combo ends on idle/hit
           → spend score on ??? → next arena mutates
```

`TBD`: what score buys. Options: new weapons, new movement verbs, world mutations, or nothing (pure leaderboard).

## Systems (skeleton)

### Movement — build this first
- Ground: run, slide, crouch-jump
- Air: Quake/Source air-strafe, so **surfing on angled ramps** works for free
- Walls: wall-run, wall-jump
- Free-fall: bonus for distance fallen, fall damage `?`
- Each verb emits a named trick event to the combo system

### Combo / style system
- Trick events append to a chain: `SURFING + WALL + FREE FALLING + SURFING`
- `points × chain length`, decays when idle
- Repeating the same trick gives diminishing returns (forces variety)

### Arsenal
- Hotbar with ammo counts (ref 1): start with 3, expand to ~10
- Draft list: plasma, cannon, rocket, homing, minigun, rail, EMP, nuke
- Each weapon should do something to **movement** too (rocket jump, rail knockback, EMP freezes ramps?)

### Enemies
- One loud colour per enemy family against a calmer world (ref 1)
- First enemy: the fanged blob. Floats, swarms, dies in one satisfying pop.

### Surreal layer (the HUD that lies)
- Organic frame around the viewport (ref 2–3)
- Corner portraits that react to combo/health (ref 4–5)
- Side feeds `?` (Q4)
- Per-level palette inversions, texture swaps mid-fight

## Tech (recommendation, not decided)

- **Engine: Godot 4.** Free, light, fast to iterate solo, and Cruelty Squad shipped on Godot, so the aesthetic is proven there. Alternative: Unity if Colin already knows it.
- Textures: phone photos of real clay/objects → tiling textures. Cheap and on-brand.
- Platforms: PC first. `TBD`.

## Milestones

| # | Milestone | Done when |
|---|---|---|
| 0 | **Movement toy** | A grey box with ramps, walls and a pit feels good to move in for 10 minutes with no enemies and no guns. If this isn't fun, nothing else matters. |
| 1 | Combo system | Tricks name themselves and multiply on screen |
| 2 | Vertical slice | 1 arena, 2 weapons, 1 enemy, the haunted HUD frame, 1 clay texture set |
| 3 | Playtest | Someone who isn't Colin plays it without being told how |
| 4+ | Content | `TBD` after the slice |

## Open questions for Colin

1. **Experience and team:** have you shipped a game or used an engine before? Solo?
2. **Engine:** Godot (recommended), Unity, Unreal, or something else?
3. **Player identity:** is the player a zombie (green hands, repo name), or is that just a vibe?
4. **Split-screen feeds:** a mechanic, a joke, or not part of this?
5. **Structure:** arena runs, linear levels, or one big interconnected world?
6. **Names of the games in refs 1 and 4–5?** Ref 2–3 is Cruelty Squad; the others weren't identified.
7. **The rest of your examples:** drop them in, and they get a row in the reference table.
