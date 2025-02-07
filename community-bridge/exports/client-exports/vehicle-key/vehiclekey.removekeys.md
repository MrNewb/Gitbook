---
description: This will Remove keys to a vehicle
---

# VehicleKey.RemoveKeys

```
local Bridge = exports.community_bridge:Bridge()

Bridge.VehicleKey.RemoveKeys(vehicle, plate)


local exampleWithVehicle = GetVehiclePedIsIn(PlayerPedId(), false)
Bridge.VehicleKey.RemoveKeys(vehicle, nil)


local exampleWithPlate = GetVehiclePedIsIn(PlayerPedId(), false)
local plate = GetVehicleNumberPlateText(exampleWithPlate)
Bridge.VehicleKey.RemoveKeys(nil, plate )
```
