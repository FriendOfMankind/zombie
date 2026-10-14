# zombie: plan skeleton

Status: **skeleton v2** *(2026-10-14)*. `TBD` = not decided. `?` = a guess waiting on Colin.

## Pitch

**Doom Eternal on a bad trip, played straight as a joke.** A round-based arena FPS that takes every videogame-ism to the extreme: MEGA BOOST, power-ups falling from the sky, a screaming announcer, combo ranks and stacking items. Your loadout is random and keeps changing, the screen is full of numbers, and creepy stuff keeps barging into the HUD and squashing the game out of the way.

The joke is the genre itself. The game has to *mock* videogames while still *being* a good one. Otherwise it's a meme that people uninstall after 10 minutes.

## Decided

| Decision | Answer | Source |
|---|---|---|
| Engine | **Godot 4** | Colin, 2026-10-14 |
| Player is a zombie? | **No.** Something else freaky, `TBD` | Colin, 2026-10-14 |
| Things barging into the HUD | **Yes, core feature.** Creepy stuff pops up and squashes the game frame out of proportion | Colin, 2026-10-14 |
| Structure | **Round-based arenas** (recommended), with platforming inside them via movement items. Pure platformer `?` | Claude recommendation, needs confirming |

## References

| Ref | What it is | Steal |
|---|---|---|
| Green cube maze, orange fanged blobs | `?` unidentified | Enemies in one loud colour against a calm world, a big weapon hotbar with ammo counts, a DPS meter |
| Cruelty Squad | Consumer Softproducts | A HUD frame made of meat, colour as an assault, ugly on purpose |
| Clay world, "SURFING + WALL + FREE FALLING × 12" | `?` unidentified | Named trick chains with a multiplier, clay textures, freaky viewmodel hands |
| Neon item grid, "CHOOSE UPGRADE", ELAPSED / THREAT | `?` unidentified (Risk of Rain 2-style item stacks) | **A wall of stacked item icons with ×2, ×3, ×4 counts**, a level-up choice screen, kill feed, a threat timer that rises |
| Red flesh floor, eyeballs, SANITY bar, $1000 | `?` unidentified | A **sanity meter**, a cash counter, a meat world, a heart in the middle of the hotbar |
| Red-haired girl, grey stick zombies in a park | `?` unidentified | Bargain-bin asset-store energy (unpolished stock assets as a deliberate joke) |
| Kingdom Hearts 1 (Traverse Town) | Square Enix | **The JRPG command menu** (Attack / Magic / Items) and circular HP/MP gauges, ripe for parody in an FPS |
| Pink bald head, skeletons, "11" combo counter | `?` unidentified | A giant combo counter in the middle of the screen, a grotesque mascot-style protagonist |
| **Sparedevil** | Sludge Pipe Games, 2024 *(source: Steam store page, 2026-10-14)* | See below |

### Sparedevil: what it actually does
*(source: Steam store page, read 2026-10-14)*

It's an arcade FPS where you bowl at evil pins, styled like '90s bowling-alley animations.
- **Bowling rules are the combo system:** knocking all 10 pins in one shot is a Strike, finishing them on the second shot is a Spare. Your rank climbs from **D to S**, and S gives a **5× score multiplier**, but you only keep it by staying fast.
- **You level up from points and pick from 40+ upgrades:** perks, different balls and secondary weapons.
- **Ball powers:** charge-and-release throws, a jump-slam ("ball-splosion"), and throwing upward at flying targets.
- **8 pin enemies, each with its own behaviour:** rocket pins that chase you, mortar pins, and **Joker pins that destroy your combo when you knock them down.**
- Global and friends leaderboards.

**Steal from it:** a real-world sport's scoring rules hijacked as the combo system, and **enemies that attack your score instead of your health.** That second one is the most useful idea in the whole reference pile.

## Pillars

1. **Every videogame-ism, cranked to 11.** If a game has done it, we do it louder and announce it.
2. **You never get to settle.** Your loadout is random and small, and it rotates. Adapt or die.
3. **The screen is under attack too.** The HUD, the frame and the UI are enemies.
4. **Readable under the noise.** Enemies and threats must still read in all the chaos. Without this, it's a screensaver.

## Core loop

```
ROUND START (announcer screams)
  → fight waves in an arena with 2 weapons + 2 movement items + 1 power-up slot
  → items drop: from the sky (supply drop), from chests, from enemies
  → style rank climbs D → C → B → A → S → SSS → ???
  → round boss / survival timer ends the round
CHOOSE UPGRADE (pick 1 of 3, RoR2-style stacking)
  → slot-machine reroll of part of your loadout
  → next round: arena mutates, threat rises
DEATH → score screen mocking you → instant restart
```

## Item design: build it like Risk of Rain, not like Doom

Pushback: "a ton of stupid stuff" is how solo projects die. If every item is bespoke code, you'll ship 12 items in a year. Instead, **items are small modifiers that hook into a handful of events**, so most new items are a data file plus a few lines:

`on_hit · on_kill · on_jump · on_land · on_pickup · on_reload · on_damage_taken · on_combo_rank_up · on_round_start`

Every item also gets a **rarity**, a **stack rule** (what ×2 does) and a **screaming name**.

### Slots (small on purpose, so randomness matters)
- **2 weapons**, **2 movement items**, **1 power-up** (timed or one-shot), plus unlimited **passive stacking items** from the upgrade screen

### Starter pool (draft, ~40)

**Weapons:** rocket launcher, super shotgun with a meat hook, railgun, minigun that slows you while you fire, BFG-style nuke ball, bowling ball (thanks, Sparedevil), homing bees, a gun that fires smaller guns, a sniper that only works mid-air, a confetti cannon (does no damage, enemies get stunned from embarrassment)

**Movement:** grapple hook, double/triple/∞ jump, air dash, wall-run, slide, ground pound, **MEGA BOOST** (a speed pad you throw down), rocket-jump boots, bunny-hop perk (no speed cap), a glider made of a flattened enemy

**Power-ups (timed):** QUAD DAMAGE, berserk (melee only, huge fists), invincibility star with the music change, bullet time, giant mode, tiny mode, **2X EVERYTHING** (enemies too), vampire, "HD textures" (the whole game briefly gets photoreal and that's somehow worse)

**Doom Eternal's resource loop, exaggerated:** chainsaw for ammo, burning for armour, glory kills for health. Make it a *slot machine*: every glory kill spins three reels, and the result decides what drops.

**Mocking classics (one-shot gags that are also real mechanics):**
- **Kingdom Hearts command menu:** an item that freezes time and makes you choose Attack / Magic / Items from a JRPG menu mid-firefight
- **QTE parody:** "PRESS F TO RESPECT", and enemies within range die of respect
- **Achievement popups** that cover the screen *during* combat ("ACHIEVEMENT: Got hit"). Some actually buff you.
- **Loading-screen tips** sliding in mid-fight, and some of them lie
- **A collectible counter:** 1/9,999 feathers, and collecting them does nothing (until it does)
- **A level-up flood:** 15 "LEVEL UP!" banners at once, each one slightly squashing the viewport
- **A boss health bar 4 screens wide** that scrolls off the edge

### Enemies that attack the game, not just you (borrowed from Sparedevil's Joker pins)
- **Combo thief:** killing it resets your style rank
- **UI eater:** chews a hole in your HUD, so you lose the ammo counter until you kill it
- **Popup:** a creepy face bursts into the HUD frame and squashes the viewport while it's alive
- **Item mimic:** looks like a chest and steals a movement item
- **Announcer's favourite:** the announcer cheers for *it* instead of you

## The HUD-intrusion system (the signature feature)

How it works in Godot: render the 3D world into a `SubViewport` and show it in a `TextureRect` inside a UI layout. Then anything that enters the layout (a face, a popup, a fake ad, a second gameplay feed) **physically shoves the game view**: it shrinks, stretches non-uniformly and gets pushed to a corner. A short tween makes it feel like getting jostled.

- **Intrusion types:** creepy faces, Gerald Ford-style found footage, a fake ad, a second unrelated "brainrot" feed, a wall of item icons
- **Severity scales with the round's THREAT level** and with the SANITY meter (from the flesh-world ref)
- **Hard rule:** the gameplay view never drops below ~50% of the screen, and the crosshair stays in its centre. It's an assault, but you can still play through it.

## Milestones

| # | Milestone | Done when |
|---|---|---|
| 0 | **Movement + shooting toy** | A grey-box arena with a grapple, a rocket launcher and a dash feels good for 10 minutes with dumb target dummies |
| 1 | **Item event system** | 10 items built entirely from event hooks, stacking works, plus a pickup-from-the-sky drop |
| 2 | **One round** | Waves, 2 enemy types, the style rank, a CHOOSE UPGRADE screen, death and instant restart |
| 3 | **HUD intrusions** | The SubViewport squash works, with 3 intrusion types tied to THREAT |
| 4 | **Vertical slice** | 3 rounds, 25 items, 1 combo-thief enemy, the announcer and one ugly texture set. Someone else plays it. |
| 5+ | Content | `TBD` after the slice |

## Open questions for Colin

1. **Round-based arena or platformer?** I'm recommending arena rounds with platforming movement inside them. A pure platformer fights the random loadouts.
2. **Who's the player?** Not a zombie, you said, so some other freaky thing. A bowling pin? A sentient meat hand? A mascot suit with nobody inside?
3. **Is there a story/world**, or just "round 1, round 2" with an announcer? Mocking videogames suggests a fake, overwrought lore dump that nobody asked for.
4. **Single player only?** Leaderboards (like Sparedevil's)?
5. **Names of the unidentified refs:** the neon item grid, the flesh/sanity game, the park zombies and the pink-head skeleton game. I won't guess.
6. **Have you built anything in Godot before?** If not, milestone 0 includes learning Godot, and that's fine, but it isn't a weekend.
