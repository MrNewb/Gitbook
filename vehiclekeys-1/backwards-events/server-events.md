---
description: Supported qb-vehiclekeys server-side backwards-compatibility events.
---

# Server Events

{% hint style="warning" %}
These are compatibility events for legacy scripts and can be disabled in config.overrides. For new development, use the [server exports](../vehicle-keys-exports/server-exports.md) instead.
{% endhint %}

### qb-vehiclekeys:server:AcquireVehicleKeys

Gives the triggering player keys for a vehicle by plate.

```lua
local plate = "PLATE123"
TriggerServerEvent('qb-vehiclekeys:server:AcquireVehicleKeys', plate)
```

### qb-vehiclekeys:server:GiveVehicleKeys

Gives the triggering player keys for a vehicle by plate.

```lua
local plate = "PLATE123"
TriggerServerEvent('qb-vehiclekeys:server:GiveVehicleKeys', plate)
```

