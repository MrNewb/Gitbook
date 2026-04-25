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

Opens the admin key management menu.

```
/vehiclekeyAdmin
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

### /fob

Opens the keyfob UI for the closest vehicle (or the vehicle the player is currently in), provided the player has keys to it.

```
/fob
```

{% hint style="info" %}
Only available when **not** using item-based keys.
{% endhint %}
