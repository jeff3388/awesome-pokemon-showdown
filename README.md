# Awesome Pokémon Showdown [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of tools, resources, plugins, datasets, and communities built around Pokémon Showdown — the most widely used competitive Pokémon battle simulator.

Maintained by the community. Pull requests welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

**Last updated:** 2026-04-08

---

## Contents

- [Getting Started](#getting-started)
- [Core Repositories](#core-repositories)
- [Damage Calculators](#damage-calculators)
- [Team Builders](#team-builders)
- [Data & Analysis Tools](#data--analysis-tools)
- [Bots & Automation](#bots--automation)
- [VGC-Specific Resources](#vgc-specific-resources)
- [Communities](#communities)
- [Self-Hosting](#self-hosting)

---

## Getting Started

| Resource | Description |
|----------|-------------|
| [pokemonshowdown.com](https://pokemonshowdown.com) | The main Pokémon Showdown client — play VGC, Smogon formats, and random battles in-browser |
| [PS! Dex](https://dex.pokemonshowdown.com) | Built-in Pokédex with competitive move, ability, and item data |
| [Damage Calculator](https://calc.pokemonshowdown.com) | Official Smogon damage calculator integrated with PS |
| [PS! Teambuilder](https://pokemonshowdown.com/teambuilder) | Browser-based teambuilder with legality checking and import/export |

### Playing VGC on Showdown

1. Go to [pokemonshowdown.com](https://pokemonshowdown.com)
2. Click **Play** → **Find a Battle** → Select **[Gen 9] VGC 2025 Reg G**
3. Or use **Teambuilder** to build and test before ladder play

---

## Core Repositories

| Repo | Description | Stars |
|------|-------------|-------|
| [smogon/pokemon-showdown](https://github.com/smogon/pokemon-showdown) | The main PS battle simulator engine — Node.js, open source, self-hostable | ⭐ 4k+ |
| [smogon/pokemon-showdown-client](https://github.com/smogon/pokemon-showdown-client) | The web client (HTML/CSS/JS) you see at pokemonshowdown.com | ⭐ 1k+ |
| [smogon/damage-calc](https://github.com/smogon/damage-calc) | Source for the Smogon damage calculator. Includes all Gen 9 mechanics. | ⭐ 700+ |
| [pkmn/ps](https://github.com/pkmn/ps) | Extracted, typed TypeScript packages from PS — use PS components without the full server | ⭐ 200+ |

---

## Damage Calculators

| Tool | Description | Supports VGC |
|------|-------------|-------------|
| [Smogon Damage Calc](https://calc.pokemonshowdown.com) | Official PS damage calculator. Supports Tera, spread moves, all Gen 9 modifiers. | ✅ |
| [pokestats.cc Damage Calculator](https://pokestats.cc/pokedex/damage-calculator) | VGC Level 50 damage calculator showing all 15 rolls with OHKO indicators | ✅ VGC-focused |
| [@pkmn/calc](https://github.com/pkmn/dmg) | TypeScript library implementing the full damage formula for all generations | ✅ |

### Using @pkmn/calc for VGC

```typescript
import { Generations } from '@pkmn/data';
import { Dex } from '@pkmn/dex';
import { calculate, Pokemon, Move } from '@pkmn/calc';

const gen = new Generations(Dex).get(9);
const atk = new Pokemon(gen, 'Koraidon', {
  nature: 'Adamant', evs: { atk: 252 }, item: 'Life Orb'
});
const def = new Pokemon(gen, 'Incineroar', { evs: { hp: 252 } });
const move = new Move(gen, 'Collision Course');
const result = calculate(gen, atk, def, move, { gameType: 'Doubles' });
console.log(result.desc());       // Human-readable result
console.log(result.range());      // [minDmg, maxDmg]
console.log(result.kochance());   // OHKO probability
```

---

## Team Builders

| Tool | Description |
|------|-------------|
| [PS! Teambuilder](https://pokemonshowdown.com/teambuilder) | Official browser teambuilder with format legality checking and Showdown paste import/export |
| [Pikalytics Team Builder](https://pikalytics.com) | Usage-data-informed teambuilder — shows how common each move/item/spread is at high ladder |
| [Pokemon Showdown Import Format](https://smogon.com/forums/threads/how-to-import-a-team.3655274/) | Guide to importing team pastes from team reports into PS |

### Showdown Team Paste Format

```
Incineroar @ Assault Vest
Ability: Intimidate
Level: 50
Tera Type: Water
EVs: 252 HP / 4 Atk / 100 Def / 148 SpD / 4 Spe
Careful Nature
- Fake Out
- Knock Off
- Flare Blitz
- Parting Shot
```

---

## Data & Analysis Tools

| Tool | Description |
|------|-------------|
| [Smogon Usage Stats](https://www.smogon.com/stats/) | Monthly ladder usage statistics for all PS formats including VGC |
| [Pikalytics](https://pikalytics.com) | Real-time usage rates from ranked VGC ladder — moves, items, teammates, spreads |
| [PS! Replay Viewer](https://replay.pokemonshowdown.com) | Browse and share battle replays. Useful for studying high-level VGC gameplay |
| [smogon/pokemon-showdown data/](https://github.com/smogon/pokemon-showdown/tree/master/data) | Raw competitive data: learnsets, formats, move effects, item data in JS format |

---

## Bots & Automation

| Project | Description | Language |
|---------|-------------|---------|
| [pmariglia/showdown](https://github.com/pmariglia/showdown) | Python bot that plays on PS automatically using heuristics | Python |
| [hsahovic/poke-env](https://github.com/hsahovic/poke-env) | Python environment for training reinforcement learning agents on PS | Python |
| [dramamine/leftovers-again](https://github.com/dramamine/leftovers-again) | Node.js PS bot framework for building custom ladder bots | Node.js |

### poke-env Quick Start (RL Agent)

```python
import asyncio
from poke_env.player import RandomPlayer, SimpleHeuristicsPlayer

async def main():
    player1 = RandomPlayer(battle_format="gen9vgc2025regg")
    player2 = SimpleHeuristicsPlayer(battle_format="gen9vgc2025regg")
    await player1.battle_against(player2, n_battles=10)
    print(f"Player 1 win rate: {player1.win_rate:.2%}")

asyncio.run(main())
```

---

## VGC-Specific Resources

| Resource | Description |
|----------|-------------|
| [Gen 9 VGC 2025 Reg G Format](https://dex.pokemonshowdown.com/formats/gen9vgc2025regg) | PS format page for current Regulation G — shows legal Pokémon and rules |
| [VGC Usage Stats (Smogon)](https://www.smogon.com/stats/2025-03/gen9vgc2025regg-1760.txt) | High-ladder VGC usage data (replace date for latest month) |
| [Pikalytics VGC](https://pikalytics.com/pokedex/gen9vgc2025regg) | Ranked VGC-specific usage with teammate and spread data |
| [pokestats.cc VGC Guides](https://pokestats.cc/guides) | Strategy guides for top Regulation G Pokémon — Incineroar, Koraidon, Flutter Mane, and more |

### Useful PS Slash Commands for VGC

```
/tier gen9vgc2025regg        Check if a Pokémon is legal in current VGC
/data [move name]            Look up move BP, type, and effects
/calc                        Open damage calculator
/roomintro vgc               View the VGC room introduction and rules
/rank                        Check your current ladder ranking
/challenge [username], gen9vgc2025regg   Challenge a specific user to VGC
```

---

## Communities

| Community | Platform | Description |
|-----------|----------|-------------|
| [Smogon VGC Forum](https://www.smogon.com/forums/forums/vgc.197/) | Forum | Strategy discussion, team rating, format analysis |
| [PS! VGC Room](https://pokemonshowdown.com/rooms/vgc) | In-client | Real-time VGC discussion and practice partner finding |
| [Victory Road Discord](https://victoryroadvgc.com/discord) | Discord | Premier competitive VGC community |
| [r/VGC](https://www.reddit.com/r/VGC/) | Reddit | 100k+ member community for team sharing and discussion |

---

## Self-Hosting

Run your own private Pokémon Showdown server:

```bash
# Clone and install
git clone https://github.com/smogon/pokemon-showdown
cd pokemon-showdown
npm install

# Start the server
node pokemon-showdown start --no-security

# Access at http://localhost:8000
# Connect client: https://play.pokemonshowdown.com/?server=localhost&port=8000
```

**Use cases for self-hosting:**
- Private team testing without public ladder exposure
- Running a club or team's internal practice server
- Custom format development and testing

---

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to suggest new tools, bots, or community resources.

**Inclusion criteria:**
- Actively maintained (updated within 2 years or permanently stable)
- Directly related to Pokémon Showdown usage or development
- Free or open source

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

Released under CC0. Use and share freely.
