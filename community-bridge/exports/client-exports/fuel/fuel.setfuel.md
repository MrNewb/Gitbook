---
description: This will set the fuel of a vehicle
---

# Fuel.SetFuel

```
local Bridge = exports.community_bridge:Bridge()


local exampleWithVehicle = GetVehiclePedIsIn(PlayerPedId(), false)
-- vehicle, fuel level (100 as an example), type of fuel (for some fuel systems, it will defualt without the param)
Bridge.Fuel.SetFuel(exampleWithVehicle, fuel, type)

```
