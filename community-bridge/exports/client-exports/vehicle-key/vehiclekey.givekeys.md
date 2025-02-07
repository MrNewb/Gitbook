---
description: This will grant keys to a vehicle
---

# VehicleKey.GiveKeys

```
local Bridge = exports.community_bridge:Bridge()

Bridge.VehicleKey.GiveKeys(vehicle, plate)


local exampleWithVehicle = GetVehiclePedIsIn(PlayerPedId(), false)
Bridge.VehicleKey.GiveKeys(vehicle, nil)


local exampleWithPlate = GetVehiclePedIsIn(PlayerPedId(), false)
local plate = GetVehicleNumberPlateText(exampleWithPlate)
Bridge.VehicleKey.GiveKeys(nil, plate )
```
