---
description: This is a list of the available server side exports.
---

# Server Exports

## GiveKeysByPlate

```lua
-- This export will give a player keys to a vehicle server side by the plate
-- plate is a string ie ("PLATENUMBER")
exports.MrNewbVehicleKeys:GiveKeysByPlate(source, plate)
```

## GiveKeys

```lua
-- This export will give a player keys to a vehicle server side
-- you must pass the player source and networkid to the vehicle
-- In this example vehicle is a variable, this should be the vehicle you want the keys for
local netId = NetworkGetNetworkIdFromEntity(vehicle)
exports.MrNewbVehicleKeys:GiveKeys(source, netId)
```

## RemoveKeysByPlate

```lua
-- This export will remove a players key to a vehicle server side
-- you must pass the player source and platestring to the vehicle
-- In this example plate is a variable, this should be the text of the plate you want to remove the keys for

local plate = "platestringhere"
exports.MrNewbVehicleKeys:RemoveKeysByPlate(source, plate)
```

## RemoveKeys

```lua
-- This export will remove a players key to a vehicle server side
-- you must pass the player source and networkid to the vehicle
-- In this example vehicle is a variable, this should be the vehicle you to remove the keys for

local netId = NetworkGetNetworkIdFromEntity(vehicle)
exports.MrNewbVehicleKeys:RemoveKeys(source, netId)
```

## HasKeysByPlate

```lua
-- This export will return if a player has keys for a vehicle
-- you must pass the player source and plate string of the vehicle
-- In this example vehicle is a variable, this should be the vehicle you want the keys for

local plate = "platestringhere"
exports.MrNewbVehicleKeys:HasKeysByPlate(source, plate)
```

## HaveKeys

```lua
-- This export will return if a player has keys for a vehicle
-- you must pass the player source and networkid to the vehicle
-- In this example vehicle is a variable, this should be the vehicle you want the keys for

local netId = NetworkGetNetworkIdFromEntity(vehicle)
exports.MrNewbVehicleKeys:HaveKeys(source, netId)
```

## SetVehicleLock

```lua
-- This export will set the lock status for a vehicle
-- you must pass the networkid of the vehicle and a lock status
-- passing 2 would lock
-- passing 1 would unlock
-- In this example vehicle is a variable, this should be the vehicle you want the keys for

local netId = NetworkGetNetworkIdFromEntity(vehicle)
exports.MrNewbVehicleKeys:SetVehicleLock(netId, 2)
```
