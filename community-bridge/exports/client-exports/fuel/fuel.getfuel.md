---
description: This will get the fuel of a vehicle
---

# Fuel.GetFuel

```
local Bridge = exports.community_bridge:Bridge()


local exampleWithVehicle = GetVehiclePedIsIn(PlayerPedId(), false)
local fuelLevel = Bridge.Fuel.GetFuel(exampleWithVehicle)
print(fuelLevel) -- returns the fuel level in the vehicle

```
