---
description: Supported qb-vehiclekeys server-side backwards-compatibility events.
---

# Server Events

{% hint style="warning" %}
These are compatibility shims for legacy scripts. For new development, use the [server exports](../vehicle-keys-exports/server-exports.md) instead.
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

