# SNS Creatures

A supernatural race, transformation, and ability system for **FiveM / Qbox**, created for Streets & Sorcery.

Assign creature races, customize alternate forms, manage six progression tiers, and use race-specific abilities powered by Aetherium.

## Features

- Race and tier persistence through Qbox player metadata.
- Transform and mutate forms with saved Illenium Appearance customization.
- Tier names from **0–5**, with elder transformation models selected at tier 5.
- Modular passive and active abilities with cooldowns and configurable key bindings.
- Aetherium reserves, regeneration, and exports for other resources.
- Vampire sunlight damage with configurable item, umbrella, and vehicle-tint protection.
- Tier-based flight-speed selection and server-side wing-access callbacks for compatible flight resources.
- An ox_lib form menu, notifications, and transformation effects.

## Requirements

| Resource | Purpose |
| --- | --- |
| `qbx_core` | Player data, metadata, and persistence |
| `ox_lib` | Callbacks, menus, notifications, and asset loading |
| `oxmysql` | Library referenced by the resource manifest |
| `illenium-appearance` | Appearance editing, saved forms, and restoring the normal skin |
| `ox_inventory` | Inventory checks for protective items |

Custom creature ped models must be installed separately. Flight requires a compatible external resource implementing the MathStore-style `flight:activateWithPresetNoBucketCheck` event; this resource does not include flight or wing assets.

Although `Config.Framework` exists, the implementation calls `qbx_core` directly. Changing that setting alone does not add standalone QB-Core support.

## Installation

1. Place this folder in your server's resources directory and keep its name **`sns_creatures`**.
2. Install the dependencies and the custom ped models you intend to use.
3. Merge the supplied [Illenium appearance snippet](<Illenium appearance snippet>) into your version of Illenium Appearance. It exposes `ForceClothMenu` and routes forced customization saves to `sns_creatures:client:saveFormAppearance`. Adapt the existing functions rather than adding duplicate definitions.
4. Review [shared/config.lua](shared/config.lua), replacing placeholder models and tier names for your server.
5. Start the resource after its dependencies. Add this to your existing startup configuration, preserving the dependencies' own required order:

   ```cfg
   ensure oxmysql
   ensure ox_lib
   ensure qbx_core
   ensure ox_inventory
   ensure illenium-appearance
   # Start your custom ped and compatible flight resources here.
   ensure sns_creatures
   ```

No separate SQL migration is included. Creature data uses the existing Qbox player metadata fields `creatureRace`, `creatureTier`, `creatureForms`, and `aetherium`.

## Commands and controls

| Command | Action |
| --- | --- |
| `/race` | Display your race |
| `/showtier` | Display your race and tier name |
| `/raceform` | Open the transformation menu |
| `/transform` | Enter your configured transformation form |
| `/mutate` | Enter your configured mutation form |
| `/revert` | Restore your normal appearance |
| `/editform transform` | Edit and save your transformation appearance |
| `/editform mutate` | Edit and save your mutation appearance |
| `/mana` | Display Aetherium reserves |
| `/useAbility` | Use the selected active ability |
| `/cycleAbility` | Select the next active ability |
| `/flightspeed [1-3]` | Select an unlocked flight speed; omit the number to cycle |

Default keys are **Z** to use an ability, **X** to cycle abilities, and **K** to cycle flight speeds. These use FiveM key mappings and can be rebound by players.

Transforming or mutating costs **25 stamina**. The first use of a form opens its appearance editor; save the customization to reuse it later.

### Race and tier management

| Command | Action |
| --- | --- |
| `/setrace [playerId] [race]` | Assign a race from `Config.Races` |
| `/removerace [playerId]` | Clear a player's race |
| `/settier [playerId] [0-5]` | Assign a creature tier |
| `/removetier [playerId]` | Clear a player's tier |

These commands currently run in-game only. **The supplied handlers do not enforce staff permissions**: they are registered as unrestricted commands without authorization checks. Add server-side permission checks before exposing them on a public server.

Example setup:

```text
/setrace 12 maleursar
/settier 12 2
```

## Races and abilities

The following races have ability modules in this copy:

| Race IDs | Example abilities |
| --- | --- |
