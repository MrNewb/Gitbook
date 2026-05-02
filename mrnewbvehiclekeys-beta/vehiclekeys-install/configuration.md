---
description: Full configuration reference for MrNewbVehicleKeys.
icon: settings
---

# Configuration

Most servers only need to adjust a small part of this page. Start with your key mode, keybinds, locksmith settings, and any shared fleet setup, then come back for the deeper sections if needed.

If this is your first setup, finish the [install steps](README.md), framework setup, and inventory items first.

## Start Here

Use this page in this order:

1. Pick whether your server is item-based or non-item-based in `ItemBasedSettings`.
2. Review `Keybinds`, `Blacklist`, and `LockSmith`.
3. Only dig into the supporting files if you are changing integrations, buttons, dispatch payloads, or minigame behavior.

## Choose Your Path

If you are not sure which parts matter to you, use the path that matches your server:

### Item-Based Servers

Start with these sections:

* `ItemBasedSettings`
* `LockSmith`
* `Keybinds`
* `KeyJobStorages` if you use shared fleets

### Non-Item-Based Servers

Start with these sections:

* `ItemBasedSettings`
* `Keybinds`
* `Blacklist`
* `VehicleSettings`

### Theft-Heavy Servers

Start with these sections:

* `Hotwire`
* `Lockpicks`
* `SearchForKeys`
* `Dispatch`

### Migration / Advanced Setups

Only open these when you actually need them:

* `Manifest Provides`
* `overrides.lua`
* `buttons.lua`
* `dispatch.lua`
* `vehicletypes.lua`

---

## Recommended First Pass

Most servers launch cleanly after reviewing these sections:

1. `Config.ItemBasedSettings` for physical keys vs virtual keys.
2. `Config.Keybinds` for default player controls.
3. `Config.Blacklist` for vehicles that should bypass or ignore theft logic.
4. `Config.LockSmith` for spare keys, keyrings, upgrades, and pricing.
5. `Config.Dispatch` and `Config.KeyJobStorages` if you use alerts or shared fleet access.

## Safe To Ignore At First

Most first-time setups do **not** need to touch these right away:

* `Core Toggles`
* `CustomCarsMissingLabels`
* `ParkingSpots`
* `Manifest Provides`
* `vehicletypes.lua`

Come back to those only if you have a clear reason.

---

## Main Config Sections

This page is grouped by what you are actually tuning: initial setup, normal vehicle access, theft gameplay, then world services and integrations.

### Setup Basics

#### Core Toggles

These are the small global switches most servers leave alone after first setup.

| Setting | What it does |
| --- | --- |
| `Config.DebugMode` | Developer-focused debug output. Leave this off unless you are troubleshooting a ticketed issue. |
| `Config.EnableUI` | Enables the custom UI features, including the keyfob interface where applicable. |

#### ItemBasedSettings

This section defines whether your server uses physical key items.

| Setting | Description |
| --- | --- |
| `Enabled` | `true` = keys are inventory items, `false` = keys are virtual/database-backed |
| `CheckOverride` | Refresh / validation interval used by the item system |
| `EnableAftermarketLocks` | Enables the aftermarket lock item workflow |
| `IncludePlayerNameInKeyDescription` | Adds the owner name into generated key metadata |

The optional `autoKeyring` export argument only matters when `Config.ItemBasedSettings.Enabled = true`.

#### Keybinds

`Config.Keybinds` holds the default bindings presented to players. They can still be rebound through FiveM settings.

| Setting | Default |
| --- | --- |
| `OpenKeyRing` | `F2` |
| `OpenKeyFob` | `F3` |
| `LockVehicle` | `L` |
| `Hotwire` | `E` |
| `SearchVehicle` | `H` |
| `EngineToggle` | `F10` |
| `AdjustAutoPilot` | `E` |

### Vehicle Access

This section is mainly about everyday usage after the script is already working.

#### VehicleSettings

`Config.VehicleSettings` controls how ordinary vehicle access feels once a player has permission to use the car.

| Setting | Description |
| --- | --- |
| `LockSounds` | Enables lock and unlock sound feedback |
| `DisableVehicleAutoStart` | Prevents GTA/FiveM from auto-starting vehicles when entered |
| `HotwireDisabled` | Hard-disables hotwire behaviour even if the hotwire config exists |
| `EngineRemainsOnWhenExiting` | Keeps the engine running when a player gets out |
| `GiveKeysIfEngineRunning` | Auto-grants keys when entering a running vehicle as driver, with safeguards for temp/shared access |
| `SuspensionBounceEnabled` | Adds a bounce response on lock / unlock |
| `FrontTrunkVehicle` | Per-model override for vehicles that use front trunk / hood interactions |

#### Blacklist

`Config.Blacklist` is one of the most important balancing sections in the whole script. It decides which vehicles bypass the normal key loop and which ones are protected from theft actions.

Included groups:

| Group | Purpose |
| --- | --- |
| `No Key Required Vehicles` | Vehicle models that can always be used without keys |
| `No Key Required Plates` | Plate-specific exceptions |
| `Hotwire Immune Vehicles` | Models that cannot be hotwired |
| `Hotwire Immune Plates` | Plate-specific hotwire immunity |
| `Lockpick Immune Vehicles` | Models that cannot be lockpicked |
| `Advanced Lockpick Required Vehicles` | Vehicles that require the advanced item |
| `Shared Job Models` | Job fleets that should be accessible without individually granting permanent keys |
| `Shared Job Plates` | Plate-based version of shared job access |

#### CustomCarsMissingLabels

Use this section when a custom vehicle displays an ugly internal model name or no friendly label at all. Each entry maps a spawn name to a readable label.

#### ProximityLocking

`Config.ProximityLocking` enables hands-free lock behaviour.

| Setting | Description |
| --- | --- |
| `Enabled` | Enables the feature |
| `PlayerDefaults` | Default player state for the toggle |
| `LockDistance` | Distance to trigger locking while walking away |
| `UnlockDistance` | Distance to trigger unlocking while approaching |
| `StoreGracePeriod` | Delay after exit to avoid accidental lock actions while storing vehicles |

#### ParkingSpots

`Config.ParkingSpots` is runtime-populated data used by self-park and summon features. Leave the table itself alone unless you are intentionally managing generated parking spot files.

The actual saved spot definitions live in `configs/parkingspots/*.lua`.

#### KeyJobStorages

`Config.KeyJobStorages` controls job-only key storage stations, which are useful for fleets, impounds, emergency services, or any role that needs shared access to a pool of vehicle keys.

This is the section that defines key holders and deposit boxes like the `police_key_holder` and `police_key_box` examples in the default config.

| Setting | Description |
| --- | --- |
| `Enabled` | Master toggle for the system |
| `Locations` | All configured job key storage entities |
| `jobName` | A single job string or an array of allowed jobs |
| `model` | Ped or prop model to spawn / target |
| `entityType` | Usually `ped` or `object` |
| `coords` | Position and heading |
| `stashId` | Unique stash identifier used by the backing storage |
| `label` | Friendly interaction label |
| `blip` | Optional map blip configuration |

Use `KeyJobStorages` when a department should share and return keys at a world location instead of permanently duplicating them to every employee.

### Theft and Recovery

If your server does not care much about theft gameplay, you can skim this section and come back later.

#### Hotwire

`Config.Hotwire` controls the full hotwire flow: whether it is enabled, how long it takes, how many attempts a player gets, how often they can retry, whether a successful hotwire grants a permanent key, and which minigame adapter is used.

Important options:

| Setting | Description |
| --- | --- |
| `Enabled` | Master toggle for hotwiring |
| `SyncedHotwires` | Syncs hotwire state to other clients through statebags |
| `MaxHotwireAttempts` | Vehicle becomes immune after too many failed attempts |
| `GiveKey` | Grants a key after a successful hotwire |
| `Minigame.Type` | Chooses the minigame integration |
| `RequireItem.Enabled` | Reserved / incomplete item requirement path; leave off unless you are testing it intentionally |

#### SearchForKeys

`Config.SearchForKeys` controls whether abandoned or NPC vehicles can be searched for keys and loot.

| Setting | Description |
| --- | --- |
| `Enabled` | Enables searching vehicles |
| `SearchTime` | Progress duration |
| `MaxSearchAttempts` | Max number of searches per vehicle |
| `Chance` | Chance to find keys |
| `SearchableItems` | Extra items that can be rewarded during searches |

#### Lockpicks

`Config.Lockpicks` handles theft difficulty and item consumption rules.

| Setting | Description |
| --- | --- |
| `Enabled` | Master toggle for lockpicking |
| `BreakChance` | Chance for the lockpick to break |
| `BreakOnSuccess` | Also consumes the lockpick on successful picks |
| `LockpickAlarmTime` | How long the vehicle alarm sounds after a pick |
| `LockpickItem` | Basic lockpick item name |
| `AdvancedLockpickItem` | Advanced lockpick item name |
| `Minigame.Type` | Selected minigame implementation |
| `Minigame.Difficulty` | Basic difficulty |
| `Minigame.AdvancedDifficulty` | Advanced difficulty |

#### LockNpcCars

`Config.LockNpcCars` randomises whether NPC vehicles spawn locked.

| Setting | Description |
| --- | --- |
| `Enabled` | Enables NPC locking |
| `LockChance` | Percent chance an NPC vehicle is locked |
| `ImmuneModels` | Models excluded from the NPC lock roll |

### Services and Interaction

This section matters most for servers using locksmiths, dispatch, target options, or job-restricted forced entry.

#### Dispatch

`Config.Dispatch` controls the gameplay side of alerts. The actual payload format lives in `configs/dispatch.lua`.

| Setting | Description |
| --- | --- |
| `Enabled` | Master toggle |
| `AlertChances` | Per-action chance for hotwire, lockpick, and hijack alerts |
| `ReceiveAlerts` | Jobs that receive the dispatch event |

#### LockSmith

`Config.LockSmith` is the economy and services hub for the script.

It controls:

| Area | Description |
| --- | --- |
| `Enabled` | Turns the locksmith service on or off |
| `EnableKeyRing` | Enables the locksmith-side keyring service flow |
| `EnableFobUpgrades` | Allows keyfob module upgrades to be purchased |
| `FobUpgradesOnOwnedOnly` | Restricts upgrades to owned vehicles only |
| `Pricing.SpareKey` | Spare key pricing |
| `Pricing.Items` | Locksmith shop inventory like keyrings, lockpicks, and aftermarket locks |
| `Locations` | NPC or prop-based locksmith spawn points |
| `GlobalTargets` | Global locksmith target models |

If you want players to buy and manage keyrings through the locksmith flow, this is the section to review alongside your inventory item setup.

#### GlobalVehicleTargets

`Config.GlobalVehicleTargets` controls the target options attached to vehicles globally.

| Target | What it does |
| --- | --- |
| `LockVehicle` | Shows a lock option |
| `UnLockVehicle` | Shows an unlock option |
| `StartEngine` | Shows an engine-on option |
| `TurnOffEngine` | Shows an engine-off option |
| `ToggleRoof` | Shows convertible roof interaction |
| `ForceUnlock` | Shows the force-unlock action for allowed jobs |

Each entry also has its own `Enabled` toggle and `Distance` setting.

#### VehicleForceUnlock

This section controls the job-restricted forced entry system.

| Setting | Description |
| --- | --- |
| `Enabled` | Enables force unlock |
| `MaxDistance` | Server-side distance validation |
| `ProgressBar.Duration` | Action time |
| `ProgressBar.CanCancel` | Whether the progress can be cancelled |
| `ProgressBar.Animation` | Animation played during the action |
| `EnabledJobs` | Jobs allowed to perform force unlock |

## Supporting Files

These files are usually follow-up tuning, not first-pass setup.

### Manifest Provides

MrNewbVehicleKeys includes optional commented `provide` lines in `fxmanifest.lua`.

They are there to make migrations easier when you are replacing another key script and still have older resources expecting the previous resource name.

Treat `provide` as a small migration helper. Uncomment only the aliases you need, keep new integrations on the native MrNewbVehicleKeys exports, and test older dependent resources after switching over.

### Companion Config Files

#### overrides.lua

`configs/overrides.lua` contains behaviour hooks and server-policy style settings that are easy to miss if you only look at `config.lua`.

Main things in this file:

* `Config.Admin` for admin command access
* `Config.ClearOldKeys` for `/clearoldkeys`
* `Config.ValidationChecks` for custom restrictions
* `Config.VehicleSounds` and animation settings for feedback tuning
* `Config.CompatabilityEvents` for legacy compatibility hooks

#### buttons.lua

`configs/buttons.lua` defines the keyfob's default and purchaseable actions.

This is where you change default buttons, purchasable modules, action IDs, pricing, and any job restrictions on button access.

#### minigames.lua

`configs/minigames.lua` is the adapter layer that converts your selected difficulty into the format required by each minigame resource.

If you are adding or replacing a minigame integration, this is the file to edit.

#### dispatch.lua

`configs/dispatch.lua` formats outgoing alerts and maps each theft action to a message, icon, and blip setup.

Use this when you want to change the actual alert text or dispatch payload, not just the chance to send one.

#### vehicletypes.lua

`configs/vehicletypes.lua` contains classification lists for convertibles and electric vehicles. Adjust this file when a custom car needs roof support or EV-specific behaviour.

---

## Practical Examples

If the main reference still feels dense, start here and copy one small pattern at a time.

### Disable Item-Based Keys

```lua
Config.ItemBasedSettings = {
    Enabled = false,
    CheckOverride = 5000,
    EnableAftermarketLocks = true,
    IncludePlayerNameInKeyDescription = true,
}
```

### Add a Shared Job Key Storage

```lua
Config.KeyJobStorages = {
    Enabled = true,
    Locations = {
        ["mechanic_key_holder"] = {
            jobName = "mechanic",
            model = "a_m_m_business_2",
            entityType = "ped",
            coords = vector4(0.0, 0.0, 0.0, 0.0),
            stashId = "mechanic_key_stash",
            label = "Mechanic Key Holder",
        },
    },
}
```

### Auto-Store Granted Keys in a Keyring

```lua
exports.MrNewbVehicleKeys:GiveKeysByPlate(source, "PLATE123", true)
```

This only applies to item-based servers and will store the key inside an existing `keyring` item when the player has one.

---

## Final Checklist

Before calling your setup finished, verify these points:

* Your framework and inventory are installed first.
* Item-based vs non-item-based mode is intentional.
* Locksmith prices match your economy.
* Shared job models, shared plates, or `KeyJobStorages` are configured if you use fleets.
* Dispatch jobs and keybinds make sense for your server.

When testing, do one workflow at a time: spawn or retrieve a vehicle, verify access, test lock and unlock, then move on to theft mechanics, locksmith actions, and job storage. If you need support, include the section you changed and whether the server is item-based or non-item-based.