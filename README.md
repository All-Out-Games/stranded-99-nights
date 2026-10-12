# Dino Island

A cooperative island-survival game for [All Out](https://allout.game/). Gather resources, craft equipment, support the beacon, and survive the island's day/night cycle and hostile creatures. Explore points of interest, find supplies, help survivors, and prepare voyages to reach further islands.

The repository retains its earlier name, `stranded-99-nights`. The current game name in `ao.project` is **Dino Island**.

## Script architecture

| Start here | Responsibility |
| --- | --- |
| [scripts/main.csl](scripts/main.csl) | Imports, item and currency registration, `Player` state, death/downed behavior, and revival. |
| [scripts/GameManager.csl](scripts/GameManager.csl) | Lobby and round phases, day/night progression, night events, island progression, voyages, and results. |
| [scripts/IslandFramework.csl](scripts/IslandFramework.csl), [POI.csl](scripts/POI.csl) | Island structure and points of interest. |
| [scripts/ResourceNode.csl](scripts/ResourceNode.csl), [ItemManager.csl](scripts/ItemManager.csl), [ItemDrops.csl](scripts/ItemDrops.csl) | Gathering, item definitions, and world pickups. |
| [scripts/CraftingSystem.csl](scripts/CraftingSystem.csl), [CraftingStationInteractable.csl](scripts/CraftingStationInteractable.csl), [GroupStorage.csl](scripts/GroupStorage.csl) | Recipes, crafting interactions, and shared supplies. |
| [scripts/Beacon.csl](scripts/Beacon.csl), [VoyagePrep.csl](scripts/VoyagePrep.csl), [VoyageBoat.csl](scripts/VoyageBoat.csl) | Beacon resources/upgrades, voyage requirements, and travel. |
| [scripts/Mob.csl](scripts/Mob.csl), [MobSpawner.csl](scripts/MobSpawner.csl), [Survivor.csl](scripts/Survivor.csl) | Hostile creatures, spawning, and survivor interactions. |
| [scripts/Chest.csl](scripts/Chest.csl), [Merchant.csl](scripts/Merchant.csl), [LogPage.csl](scripts/LogPage.csl), [TutorialSystem.csl](scripts/TutorialSystem.csl) | Loot, trading, discoveries, and onboarding. |

`GameManager` coordinates the shared run. Resource nodes, crafting stations, storage, and the beacon turn gathering into group progress. Voyage preparation consumes the required supplies before travel advances the group to another island. Combat is supported by [scripts/reusable_weapons/](scripts/reusable_weapons/).

## How CSL works here

CSL is All Out's statically typed scripting language. The editor compiles `.csl` files for the All Out engine, and [ao.project](ao.project) selects CSL with `"csl": true`.

- `main.csl` imports `core:ao`, `core:dropped_items`, and `reusable_weapons`. `ao_before_scene_load` registers items and currency before the scene needs them.
- `Player` extends `Player_Base`. World mechanics use `Component` and `Interactable` subclasses; `@ao_serialize` fields bind them to editor-authored entities and configuration.
- Lifecycle callbacks initialize and update components. The manager tracks shared run state, while players hold their own inventory, health-related behavior, and UI state.
- All Out supplies client prediction and authoritative server reconciliation. Gathering, crafting, combat, and spawning should remain in shared gameplay so participants agree on the world. Keep local presentation derived from synchronized state, including when a player joins an existing run.

[scene/](scene/) stores the authored world and component settings, and [res/](res/) stores project assets. `scripts/.ao_core/` and `api_references/` are engine reference material; the files above are the starting points for game changes.

## Open and remix

1. Set up the [Windows All Out editor](https://docs.allout.game/getting-started/first-game).
2. Clone the project:

   ```sh
   git clone https://github.com/All-Out-Games/stranded-99-nights.git
   ```

3. Open the cloned folder containing `ao.project`. Let compilation and asset preparation finish, then press **Play**. Add local clients to try shared storage, crafting, revives, and voyage progression together.
4. To publish a remix, create your own Creator Portal game and associate the working copy with that identity. Review product IDs, purchases, progression, and balance for your version; the existing project IDs point to the original live and staging games.

Requires the All Out editor/runtime and referenced platform assets. Saving scripts triggers compilation; restart play mode after startup or scene changes. Further reading: [CSL syntax](https://docs.allout.game/scripting/syntax), [networking](https://docs.allout.game/scripting/networking-fundamentals), and [playtesting](https://docs.allout.game/getting-started/playtesting-your-game).

## License

The code, documentation, and original assets contributed by All Out Games are available under the [MIT License](LICENSE). You may copy, modify, remix, distribute, and use them in commercial games, including games published on All Out. Keep the copyright and license notice with copies or substantial portions.

Separately licensed third-party material retains its own terms. References to platform-provided assets, such as `$AO/...`, do not transfer ownership of those assets or license the All Out engine and services.
