---
description: A list of all available in-game commands.
icon: message-smile
---

# Commands

Use this page as the quick-reference sheet for admin actions, player keybinds, and a few keyring-specific behavior notes.

## Quick Reference

### Admin Commands

| Command | Usage | Description |
| --- | --- | --- |
| `/vehiclekeyadmin` | `/vehiclekeyadmin` | Open the admin key management menu |
| `/givekeys` | `/givekeys <playerID> <plate>` | Give a player keys by plate |
| `/removekeys` | `/removekeys <playerID> <plate>` | Remove a player's keys by plate |
| `/listkeys` | `/listkeys <playerID>` | Print a player's key list to console |
| `/revokekeys` | `/revokekeys <plate>` | Revoke keys for a plate from all online players |
| `/devmode` | `/devmode` | Toggle temp key bypass on your client |

### Player Keybinds

| Action | Default Key | Description |
| --- | --- | --- |
| Lock / Unlock Vehicle | **L** | Lock or unlock the closest vehicle |
| Toggle Engine | **F10** | Toggle vehicle engine on / off |
| Open Keyring | **F2** | Open keyring menu (non-item mode only) |
| Hotwire Vehicle | **E** | Attempt to hotwire a vehicle you lack keys for |
| Search Vehicle | **H** | Search a vehicle for keys and items |
| Toggle Proximity Locks | — | Toggle personal proximity locking |
| Cycle Autopilot Mode | **F11** | Cycle autopilot driving mode |
| `/clearoldkeys` | — | Remove keys for vehicles no longer in the world |

{% hint style="info" %}
All keybinds can be rebound in GTA V's **Key Bindings** settings under the **FiveM** tab.
{% endhint %}

{% hint style="success" %}
If you only need the day-to-day controls, the two sections above are enough. The rest of this page is the detailed breakdown.
{% endhint %}

---

## Admin Commands

{% hint style="warning" %}
Admin commands require the player to be flagged as an admin. This is configured via `Config.Admin.IsPlayerAdmin` in `overrides.lua`.
{% endhint %}

### /vehiclekeyadmin

Opens the in-game admin menu for key management.

{% hint style="info" %}
This is the fastest way to troubleshoot missing keys, test temporary access, and create parking spots for advanced keyfob actions.
{% endhint %}

```
/vehiclekeyadmin
```

| Menu Option | Description |
| --- | --- |
| **List All Vehicles** | Fetches all owned vehicles from the database. Selecting any entry instantly grants you keys to that vehicle. Useful for diagnosing key issues. |
| **Grant Key by Plate** | Opens a text input — type any plate string to grant yourself keys immediately. Useful when a vehicle is not in the owned vehicles list. |
| **Get Keys (Closest Vehicle)** | Scans within 10 metres and grants keys to the nearest vehicle. No plate input required. |
| **Parking Spot Creator** | Launches an interactive parking spot placement tool. Name the area, place spots one by one, then save. Results are used for the self-park keyfob action. |
| **Toggle Temp Key — All Vehicles** | Toggles the global temporary key bypass on your client. You can enter and operate any vehicle without keys. Same as `/devmode`. |
| **Grant Temp Key — Per Vehicle** | Enter a plate and optional duration (seconds) to grant a timed temp key for that specific vehicle only. |

---

### /givekeys

Gives a player keys to a specific vehicle by plate.

```
/givekeys <playerID> <plate>
```

Both the admin and the target player receive a notification.

### /removekeys

Removes a player's keys for a specific vehicle by plate. Performs a deep search inside a keyring item if present.

```
/removekeys <playerID> <plate>
```

### /listkeys

Prints a list of all keys held by the target player to the server console.

```
/listkeys <playerID>
```

### /revokekeys

Revokes keys for a specific plate from **all currently online players** at once. Useful when a vehicle is sold, stolen, or repossessed.

{% hint style="warning" %}
This affects every online player with access to that plate, so it is best used as a corrective admin action rather than a routine tool.
{% endhint %}

```
/revokekeys <plate>
```

### /devmode

Toggles the global temporary key bypass on your client. Same as the **Toggle Temp Key** option inside `/vehiclekeyadmin`.

```
/devmode
```

---

## Player Commands

### Keybinds

The following actions are bound to keys and can all be rebound in GTA V's **Key Bindings** settings under the **FiveM** tab. Default keys are set via the `Config.Keybinds` table in `configs/config.lua`.

| Action | Default Key | Config Key | Notes |
| --- | --- | --- | --- |
| Lock / Unlock Vehicle | **L** | `Config.Keybinds.LockVehicle` | Works in and out of the vehicle |
| Toggle Engine | **F10** | `Config.Keybinds.EngineToggle` | Must be seated in the vehicle |
| Open Keyring | **F2** | `Config.Keybinds.OpenKeyRing` | Non-item mode only |
| Hotwire Vehicle | **E** | `Config.Keybinds.Hotwire` | Requires `Config.Hotwire.Enabled = true` |
| Search Vehicle | **H** | `Config.Keybinds.SearchVehicle` | Requires `Config.SearchForKeys.Enabled = true` |
| Toggle Proximity Locks | — | — | Requires `Config.ProximityLocking.Enabled = true` |
| Cycle Autopilot Mode | **F11** | — | Only active while autopilot is running |

---

### /clearoldkeys

Scans the player's inventory for key items belonging to vehicles no longer present in the world and removes them.

```
/clearoldkeys
```

{% hint style="info" %}
Only available when using item-based keys. Has a cooldown (default: 30 seconds) configurable under `Config.ClearOldKeys.CooldownTime` in `overrides.lua`.
{% endhint %}

---

## Keyring Notes

{% hint style="info" %}
When using item-based keys, the server exports `GiveKeys`, `GiveKeysByPlate`, and `AddKeysByPlate` all support an optional third argument: `autoKeyring`.
{% endhint %}

If `autoKeyring` is set to `true`, the script will look for a `keyring` item in the player's inventory and place the new key directly into that keyring's metadata instead of giving the player a standalone `vehiclekeys` item.

If `autoKeyring` is omitted or `false`, the script uses the normal behavior and gives the player a regular key item.

Key removal works the same way in reverse when you opt into deep searching. `RemoveKeys` and `RemoveKeysByPlate` accept an optional `deepSearch` argument. When set to `true`, removal also checks inside the player's keyring item.

{% hint style="success" %}
For item-based servers, this is the cleanest way to keep player inventories tidy when keys are granted from garages, dealerships, rentals, or admin tools.
{% endhint %}

