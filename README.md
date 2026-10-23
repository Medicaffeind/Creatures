# Creatures

A supernatural roleplay resource for **FiveM / Qbox**, combining creature races, abilities, werewolf howls, and wing controls.

## Features

- Persistent races and six progression tiers.
- Customizable transformation and mutation appearances.
- Active/passive abilities, Aetherium, and toughness.
- Directional werewolf howls with optional GPS prompts.
- Tiered flight controls and optional wing/tail integrations.

All transformation models default to GTA male/female freemode peds. Custom models are optional.

## Requirements

OneSync, `qbx_core`, `ox_lib`, `ox_inventory`, and `illenium-appearance`, plus their dependencies. No additional SQL migration or xSound installation is required.

Howl recordings, flight engines, and third-party wing assets are **not included**. See the [integration guide](docs/INTEGRATIONS.md).

## Installation

1. Place the resource in your server's resources folder as **`creatures`**.
2. Start it after its dependencies:

   ```cfg
   ensure oxmysql
   ensure ox_lib
   ensure qbx_core
   ensure ox_inventory
   ensure illenium-appearance
   ensure creatures

   add_ace group.admin creatures.admin allow
   ```

3. Ensure your intended staff belong to `group.admin`, then assign a race and tier in-game:

   ```text
   /setrace 12 malewerewolf
   /settier 12 2
   ```

4. Use `/transform` or `/mutate` and save your appearance. Use `/revert` to restore your normal character.

## Controls

**Z** uses the selected ability, **X** cycles abilities, and **K** cycles unlocked flight speeds. Players can rebind these in FiveM settings.

| Command | Action |
| --- | --- |
| `/raceform` | Open the form menu |
| `/transform`, `/mutate`, `/revert` | Change forms |
| `/editform [transform\|mutate]` | Edit the active form |
| `/race`, `/showtier`, `/mana` | View character information |
| `/howl` | Broadcast a werewolf howl |
| `/flightspeed [1-3]` | Select an unlocked flight speed |
| `/wingflight [wingSet] [speed]` | Toggle flight through a compatible engine |

Staff commands: `/setrace`, `/removerace`, `/settier`, and `/removetier`. They require the `creatures.admin` ACE permission. See [full usage instructions](docs/USAGE.md) for arguments and details.

## Configuration

- [shared/config.lua](shared/config.lua): races, forms, tiers, sunlight, and controls.
- [shared/wings.lua](shared/wings.lua): flight access and optional adapters.
- [shared/howl.lua](shared/howl.lua): add your recordings to `sounds/` and configure `SoundUrls`.

## Documentation

[Full usage](docs/USAGE.md) · [Races and abilities](docs/RACES.md) · [Integrations](docs/INTEGRATIONS.md) · [Developer API](docs/API.md) · [Migration](docs/MIGRATION.md) · [Testing](docs/TESTING.md)

Automated checks are included; test in-game before deployment. Review the [security boundaries](SECURITY.md) and [third-party notes](THIRD_PARTY.md). No license file is supplied.
