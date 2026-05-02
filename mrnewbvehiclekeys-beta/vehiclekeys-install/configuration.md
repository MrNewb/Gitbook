---
description: Full configuration reference for MrNewbVehicleKeys.
icon: settings
---

# Configuration

MrNewbVehicleKeys is heavily configurable. Most day-to-day setup lives in `configs/config.lua`, while a few feature-specific files extend that base config.

This page is the practical map of what each section controls, what you are most likely to change first, and where the supporting config files fit in.

{% hint style="info" %}
If you are setting the script up for the first time, do the [install steps](README.md), finish your framework and inventory setup, then come back here to tune behaviour.
{% endhint %}

## Quick Navigation

| Want to change... | Jump to |
| --- | --- |
| Setup basics, key mode, and default controls | [Setup Basics](#setup-basics) |
| Vehicle access, shared fleets, and labels | [Vehicle Access](#vehicle-access) |
| Hotwire, search, and lockpick behavior | [Theft and Recovery](#theft-and-recovery) |
| Locksmith, dispatch, and vehicle interactions | [Services and Interaction](#services-and-interaction) |
| Supporting config files and migration notes | [Supporting Files](#supporting-files) |
| Copy-paste examples and rollout checks | [Practical Examples](#practical-examples), [Final Checklist](#final-checklist) |

## Config File Map

| File | What it controls |
| --- | --- |
| `configs/config.lua` | Main gameplay configuration, locksmith, targeting, dispatch, keyring, key storage, and most feature toggles |
| `configs/overrides.lua` | Admin permissions, validation hooks, command toggles, animations, compatibility events, and sound behaviour |
| `configs/buttons.lua` | Keyfob button layout, purchaseable modules, pricing, and action bindings |
| `configs/minigames.lua` | Minigame adapter logic and difficulty handling |
| `configs/dispatch.lua` | Dispatch message payloads, icons, alert formatting, and job delivery |
| `configs/vehicletypes.lua` | Convertible and electric vehicle classification lists |
| `configs/parkingspots/*.lua` | Saved self-park / summon parking zones generated or maintained per location |

---

## Recommended First Pass

If you only want to get the script production-ready fast, these are the sections most servers change first:

{% hint style="info" %}
You do not need to change everything here. Most servers only touch a handful of these sections before the first production launch.
{% endhint %}

| Priority | Section | Why it matters |
| --- | --- | --- |
| 1 | `Config.ItemBasedSettings` | Decides whether keys are physical items or stored virtually |
| 2 | `Config.Keybinds` | Changes the default player controls |
| 3 | `Config.Blacklist` | Defines vehicles that do not need keys, cannot be hotwired, or are shared by job |
| 4 | `Config.LockSmith` | Controls spare keys, keyrings, aftermarket locks, prices, and locksmith NPCs |
| 5 | `Config.Dispatch` | Controls whether police/EMS style alerts fire during theft actions |
| 6 | `Config.GlobalVehicleTargets` | Enables or disables target options for lock, unlock, engine, roof, and force unlock |
| 7 | `Config.KeyJobStorages` | Adds job-only key holders / deposit boxes for fleet or duty vehicles |

---

## Main Config Sections

This page is grouped by what you are actually tuning: initial setup, normal vehicle access, theft gameplay, then world services and integrations.

### Setup Basics

#### Core Toggles

| Setting | What it does |
| --- | --- |
| `Config.DebugMode` | Developer-focused debug output. Leave this off unless you are troubleshooting a ticketed issue. |
| `Config.EnableUI` | Enables the custom UI features, including the keyfob interface where applicable. |

{% hint style="warning" %}
`Config.DebugMode` is not a normal gameplay setting. Treat it as a troubleshooting switch.
{% endhint %}

#### ItemBasedSettings

This section defines whether your server uses physical key items.

| Setting | Description |
| --- | --- |
| `Enabled` | `true` = keys are inventory items, `false` = keys are virtual/database-backed |
| `CheckOverride` | Refresh / validation interval used by the item system |
| `EnableAftermarketLocks` | Enables the aftermarket lock item workflow |
| `IncludePlayerNameInKeyDescription` | Adds the owner name into generated key metadata |

{% hint style="info" %}
The optional `autoKeyring` export argument only matters when `Config.ItemBasedSettings.Enabled = true`.
{% endhint %}

#### Keybinds

`Config.Keybinds` holds the default bindings presented to players. They can still be rebound through FiveM settings.

{% hint style="info" %}
These are only the defaults shown to players. They can still be changed client-side in FiveM key bindings.
{% endhint %}

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

{% hint style="success" %}
Use `KeyJobStorages` when a department should share and return keys at a world location instead of permanently duplicating them to every employee.
{% endhint %}

### Theft and Recovery

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

{% hint style="info" %}
If you want players to buy and manage keyrings through the locksmith flow, this is the section to review alongside your inventory item setup.
{% endhint %}

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

### Manifest Provides

MrNewbVehicleKeys includes optional commented `provide` lines in `fxmanifest.lua`.

They are there to make migrations easier when you are replacing another key script and still have older resources expecting the previous resource name.

{% hint style="info" %}
Treat `provide` as a small migration helper. Uncomment only the aliases you need, keep new integrations on the native MrNewbVehicleKeys exports, and test any older dependent resources after switching over.
{% endhint %}

### Companion Config Files

#### overrides.lua

`configs/overrides.lua` contains behaviour hooks and server-policy style settings that are easy to miss if you only look at `config.lua`.

Notable sections:

| Section | What it controls |
| --- | --- |
| `Config.Admin` | Admin command access check |
| `Config.ClearOldKeys` | Enables and rate-limits `/clearoldkeys` |
| `Config.ValidationChecks` | Hook points for custom restrictions like cuffed/dead checks |
| `Config.VehicleSounds` | Horn/flash feedback tuning |
| `Config.AnimationSettings` | General keyfob animation |
| `Config.LockpickAnimationSettings` | Lockpick animation |
| `Config.CompatabilityEvents` | Legacy compatibility event toggles |

#### buttons.lua

`configs/buttons.lua` defines the keyfob's default and purchaseable actions.

The file controls:

| Setting | Description |
| --- | --- |
| `EnabledButtons` | Buttons available by default |
| `ExtraButtons` | Purchaseable or optional modules |
| `action_id` | Export-safe ID used by integrations |
| `price` | Locksmith upgrade cost |
| `canPurchase` | Whether the button is a purchasable module |
| `jobsAllowed` | Optional job lock for a button |

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

| Check | Why |
| --- | --- |
| Your framework and inventory are installed first | Prevents bridge auto-detection issues |
| Item-based vs non-item-based mode is intentional | Affects almost every workflow in the script |
| Locksmith prices match your economy | Prevents progression from feeling broken |
| Shared job models / plates are configured | Stops emergency and service jobs from being over-granted keys |
| Dispatch jobs are correct | Prevents alerts going nowhere |
| KeyJobStorages are configured if you use shared fleets | Gives departments a clean key handoff workflow |
| Keybinds are sensible for your player base | Avoids conflicts with other heavily used scripts |

{% hint style="warning" %}
When changing multiple interconnected systems at once, test one workflow at a time: spawn or retrieve a vehicle, verify access, test lock/unlock, then test theft mechanics, locksmith actions, and job storage separately.
{% endhint %}

{% hint style="info" %}
If you ask for support on a config issue, include the exact section you changed and whether the server is item-based or non-item-based. That usually narrows the answer down immediately.
{% endhint %}