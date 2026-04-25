---
description: Supported qb-vehiclekeys client-side backwards-compatibility events.
---

# Client Events

{% hint style="warning" %}
These are compatibility shims for legacy scripts. For new development, use the [client exports](../vehicle-keys-exports/client-exports.md) instead.
{% endhint %}

### vehiclekeys:client:SetOwner

Gives the local player ownership keys for a vehicle by plate.

```lua
local plate = "PLATE123"
TriggerEvent('vehiclekeys:client:SetOwner', plate)
```

### qb-vehiclekeys:client:AcquireVehicleKeys

Gives the local player keys for a vehicle by plate.

```lua
local plate = "PLATE123"
TriggerEvent('qb-vehiclekeys:client:AcquireVehicleKeys', plate)
```

### qb-vehiclekeys:client:AddKeys

Adds keys for a vehicle by plate to the local player's key list.

```lua
local plate = "PLATE123"
TriggerEvent('qb-vehiclekeys:client:AddKeys', plate)
```

### qb-vehiclekeys:client:RemoveKeys

Removes the local player's keys for a vehicle by plate.

```lua
local plate = "PLATE123"
TriggerEvent('qb-vehiclekeys:client:RemoveKeys', plate)
```

