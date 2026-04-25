---
icon: umbrella-beach
---

# Backwards Events

{% hint style="info" %}
These events exist for compatibility with scripts that were originally built for **qb-vehiclekeys**. If you are writing new integrations, use the [direct exports](../vehicle-keys-exports/README.md) instead — they provide access to more features.
{% endhint %}

The following qb-vehiclekeys events are supported. For each one, the recommended export replacement is shown.

### Client Events

| Legacy Event | Replacement Export |
| --- | --- |
| `vehiclekeys:client:SetOwner` | `exports.MrNewbVehicleKeys:GiveKeys(vehicle)` |
| `qb-vehiclekeys:client:AcquireVehicleKeys` | `exports.MrNewbVehicleKeys:GiveKeysByPlate(plate)` |
| `qb-vehiclekeys:client:AddKeys` | `exports.MrNewbVehicleKeys:GiveKeysByPlate(plate)` |
| `qb-vehiclekeys:client:RemoveKeys` | `exports.MrNewbVehicleKeys:RemoveKeysByPlate(plate)` |

### Server Events

| Legacy Event | Replacement Export |
| --- | --- |
| `qb-vehiclekeys:server:AcquireVehicleKeys` | `exports.MrNewbVehicleKeys:GiveKeysByPlate(src, plate)` |
| `qb-vehiclekeys:server:GiveVehicleKeys` | `exports.MrNewbVehicleKeys:GiveKeysByPlate(src, plate)` |
