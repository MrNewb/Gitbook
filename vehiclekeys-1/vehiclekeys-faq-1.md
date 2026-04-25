---
description: A list of all available in-game commands.
icon: message-smile
---

# Commands

## Admin Commands

{% hint style="warning" %}
Admin commands require the player to be flagged as an admin. This is configured via `Config.Admin.IsPlayerAdmin` in `overrides.lua`.
{% endhint %}

### /giveadminkey

Gives a player keys to a specific vehicle by plate.

```
/giveadminkey <playerID> <plate>
```

**Example:** `/giveadminkey 1 MYCOLPL8` — gives keys for plate `MYCOLPL8` to player ID `1`.

### /givenearbykey

Gives the closest player keys to the closest vehicle in range.

```
/givenearbykey
```

### /vehiclekeyAdmin

Opens the in-game admin menu for key management. Each option is described below.

```
/vehiclekeyAdmin
```

#### Menu Options

**List All Vehicles**

Fetches all owned vehicles from the database and lists them in a menu. Selecting any entry instantly grants you keys to that vehicle. Useful for testing or diagnosing key issues across the server.

**Grant Key by Plate**

Opens a text input where you can type any plate string manually. The admin is granted keys for that plate immediately. Useful when a vehicle is not in the owned vehicles list.

**Get Keys (Closest Vehicle)**

Scans for vehicles within 10 metres of the admin and grants keys to the nearest one. No plate input required.

**Parking Spot Creator**

Launches an interactive parking spot placement tool. You are prompted to name the area, then place spots one by one using an object placer. Spots are saved to the server when you choose to finish. The resulting config can be used for the self-park keyfob action.

**Toggle Temp Key — All Vehicles**

Toggles the global temporary key bypass for the admin's client. When enabled, the admin can enter and operate any vehicle without needing keys. Toggle it off when finished. This is the same as `/devmode`.

**Grant Temp Key — Per Vehicle**

Opens a form to enter a plate and an optional duration in seconds. Grants a temporary key for that vehicle only. If no duration is entered the temp key is permanent until manually removed or the resource restarts.

---

### /givekeys

Gives a player keys to a specific vehicle by plate.

```
/givekeys <playerID> <plate>
```

Both the admin and the target player receive a notification.

### /removekeys

Removes a player's keys for a specific vehicle by plate. Performs a deep search (including inventory items if item-based mode is on).

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

```
/revokekeys <plate>
```

### /devmode

Toggles the global temporary key bypass on the admin's client (same as the **Toggle Temp Key** option inside `/vehiclekeyAdmin`).

```
/devmode
```

---

## Player Commands

### /proximitylocks

Toggle personal proximity locking on or off. When enabled, vehicles automatically lock when you walk away and unlock when you approach.

```
/proximitylocks
```

{% hint style="info" %}
Proximity locks must be enabled globally in the config (`Config.ProximityLocks.Enabled = true`) before players can toggle this.
{% endhint %}

### /lockvehicle

Toggle the lock on the closest vehicle. Also bound to a keybind (default: **L**).

```
/lockvehicle
```

{% hint style="info" %}
The keybind can be changed under `Config.KeybindSettings.LockKeyBind` in the config.
{% endhint %}

### /enginetoggle

Toggle the engine of the vehicle you are currently sitting in. Also bound to a keybind (default: **G**).

```
/enginetoggle
```

{% hint style="info" %}
Engine toggle must be enabled in the config. The keybind can be changed under `Config.KeybindSettings.EngineKeyBind`.
{% endhint %}

### /keyring

Opens the keyring menu, showing all keys the player currently holds. Offers sub-menus to give, drop, or manage keys.

```
/keyring
```

{% hint style="info" %}
Only available when **not** using item-based keys (`Config.ItemBasedSettings.Enabled = false`).
{% endhint %}

### /givekeys

Gives keys for the closest vehicle to the closest player nearby. The player must already have keys to the vehicle to give them.

```
/givekeys
```

{% hint style="info" %}
Only available when **not** using item-based keys.
{% endhint %}

{% hint style="info" %}
Only available when **not** using item-based keys.
{% endhint %}

### /clearoldkeys

Scans the player's inventory for key items that belong to vehicles no longer present in the world and removes them.

```
/clearoldkeys
```

{% hint style="info" %}
Only available when using item-based keys. Has a cooldown (default: 30 seconds) to prevent abuse. The cooldown can be adjusted under `Config.ClearOldKeys.CooldownTime` in `overrides.lua`.
{% endhint %}

