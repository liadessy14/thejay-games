# Jay Avenger: SPACE ASSAULT - Technical Game Rules

## Controls
- **Desktop**: Click + drag mouse to move hero
- **Mobile**: Touch + drag finger
- **Movement limit**: Left half of screen only (X ≤ canvas.width/2 + 30)

## Weapons
| Mode | Projectiles | Damage | Duration |
|------|-------------|--------|----------|
| Normal | 1 straight shot | Standard | Always |
| Triple Laser (Power-up) | 3 shots (up/center/down) | +80% | ~400 frames |

## Scoring
```

Kill = 25 × Combo + (Level × 2)
Boss Kill = 650 × Level
Combo resets when hit by enemy or laser

```

| Combo | Multiplier |
|-------|------------|
| 1x | 1x |
| 2x | 2x |
| 3x+ | 3x+ |

## Level Progression
- **Target score start**: 650
- **Increase formula**: `target = (target × 1.65) + 650`
- **Level up rewards**: +20 Shield, Combo -1

## Enemy Types

### Regular Alien
| Property | Value |
|----------|-------|
| Movement | Straight or Zigzag |
| Speed | `3.5 + random + (level × 0.45)` |
| Shoot at | Level ≥ 2 |
| HP (Level ≥ 5) | 2 hits |
| Collision damage | -24 Shield |

### Boss (every Level 3, 6, 9...)
| Property | Value |
|----------|-------|
| HP | `(Level × 480) + 300` |
| Attack pattern | 3 spread lasers + 1 center |
| Kill reward | 650 × Level + 5 kills |

## Shield System
| Action | Effect |
|--------|--------|
| Max shield | 100 |
| Enemy collision | -24 |
| Enemy laser hit | -12 |
| Level up | +20 |
| Power-up pickup | +30 + Triple Laser |

**Game Over when shield ≤ 0**

## Power-Up (Green Jay Logo)
- **Spawn rate**: Every ~310 frames
- **Effect**: +30 Shield + Triple Laser mode
- **Movement speed**: 3.4 px/frame (left)

## Combo Rules
- **Active**: Consecutive kills without taking damage
- **Reset**: Hit by laser, enemy collision, or enemy leaves left edge
- **Level up**: Combo -1 (not full reset)

## Difficulty Scaling
| Level | Change |
|-------|--------|
| 1-2 | Enemies don't shoot |
| 3+ | All enemies shoot |
| 5+ | Some enemies have 2 HP |
| Every level | Speed +0.45, spawn delay -2.5 |

```

Spawn Delay = max(12, 44 - Level × 2.5)

```

## Collision Detection
- **Hero vs Enemy**: Circular + bounding box hybrid
- **Laser vs Enemy**: Rectangular hitbox
- **Invincibility frames**: ~20 frames after hit (blinking effect)

## Visual Feedback
| Event | Effect |
|-------|--------|
| Shoot | Blue laser |
| Hit enemy | Orange/red explosion (20 particles) |
| Power-up | Green aura + flash text |
| Level up | Yellow flash + message |
| Low shield (<35) | Shield bar turns red |

## UI Elements
| Element | Position | Color |
|---------|----------|-------|
| Score | Top-left | Yellow-white |
| Kills | Top-left row 2 | Cyan |
| Target | Top-left row 3 | Light blue |
| Level | Top-right | Gold |
| Shield bar | Upper-middle | Green/Red |
| Boss HP | Upper-right | Red |
| Combo | Top-center | Cyan/Pink |

## Technical Specs
| Parameter | Value |
|-----------|-------|
| Canvas | 800 × 500 px |
| Target FPS | 60 |
| Input | Mouse + Touch events |
| Audio | Web Audio API |
| Assets | PNG with background removal (sticker effect) |

## Game End Condition
**No win condition** — game continues until shield reaches 0. High score is the objective.
