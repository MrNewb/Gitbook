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
-- optional: deepSearch, this will search in a keyfob if you want to make sure its removed.

local plate = "platestringhere"
exports.MrNewbVehicleKeys:RemoveKeysByPlate(source, plate, deepSearch)
```

## RemoveKeys

```lua
-- This export will remove a players key to a vehicle server side
-- you must pass the player source and networkid to the vehicle
-- In this example vehicle is a variable, this should be the vehicle you to remove the keys for
-- optional: deepSearch, this will search in a keyfob if you want to make sure its removed.

local netId = NetworkGetNetworkIdFromEntity(vehicle)
exports.MrNewbVehicleKeys:RemoveKeys(source, netId, deepSearch)
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

## GrantRental

```lua
-- must pass source, plate, modelName, netId (optional netId)

exports.MrNewbVehicleKeys:GrantRental(source, plate, modelName, netId)
```

## RemoveRental

```lua
-- must pass source, plate, netId (optional netId)

exports.MrNewbVehicleKeys:RemoveRental(source, plate, netId)
```

## DisableLockPickingVehicle

```lua
-- must pass networkID of a vehicle
-- toggle is bool

exports.MrNewbVehicleKeys:DisableLockpickingVehicle(netId, toggle) -- will return bool
```

## KeyType

```lua
-- Will return true if keys are set to item based or false if not

exports.MrNewbVehicleKeys:KeyType() -- will return bool
```

## UpdateKey

```lua
-- source: player source
-- olplate: plate string of original
-- netplate: plate string of desired plate

exports.MrNewbVehicleKeys:UpdateKey(source, oldPlate, newPlate) -- will return bool
```

## GetVehicleKeyList

```lua
-- This ones wip
exports.MrNewbVehicleKeys:GetVehicleKeyList() -- will return table of all plates?
```

