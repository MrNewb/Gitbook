---
description: This is a list of the available server side exports.
---

# Server Exports

## Key Management

### GetPlayerKeys

```lua
-- Returns a table of all vehicle plates the player currently has keys for.
local keys = exports.MrNewbVehicleKeys:GetPlayerKeys(source)
for _, plate in ipairs(keys) do
    print(plate)
end
```

### GiveKeys

```lua
-- Gives a player keys to a vehicle by network ID.
local netId = NetworkGetNetworkIdFromEntity(vehicle)
exports.MrNewbVehicleKeys:GiveKeys(source, netId)
```

### GiveKeysByPlate

```lua
-- Gives a player keys to a vehicle by plate string.
exports.MrNewbVehicleKeys:GiveKeysByPlate(source, "PLATE123")
```

### AddKeysByPlate

```lua
-- Alias for GiveKeysByPlate.
exports.MrNewbVehicleKeys:AddKeysByPlate(source, "PLATE123")
```

### HasKeys

```lua
-- Returns true if the player has keys to a vehicle by network ID.
local netId = NetworkGetNetworkIdFromEntity(vehicle)
local hasKeys = exports.MrNewbVehicleKeys:HasKeys(source, netId)
print(hasKeys) -- boolean
```

### HasKeysByPlate

```lua
-- Returns true if the player has keys to a vehicle by plate string.
local hasKeys = exports.MrNewbVehicleKeys:HasKeysByPlate(source, "PLATE123")
print(hasKeys) -- boolean
```

### HaveKeys

```lua
-- Alias for HasKeys.
local netId = NetworkGetNetworkIdFromEntity(vehicle)
local hasKeys = exports.MrNewbVehicleKeys:HaveKeys(source, netId)
```

### RemoveKeys

```lua
-- Removes a player's keys to a vehicle by network ID.
-- deepSearch (optional): when true, also searches the player's inventory (item-based mode only).
local netId = NetworkGetNetworkIdFromEntity(vehicle)
exports.MrNewbVehicleKeys:RemoveKeys(source, netId)
exports.MrNewbVehicleKeys:RemoveKeys(source, netId, true) -- deep search
```

### RemoveKeysByPlate

```lua
-- Removes a player's keys to a vehicle by plate string.
-- deepSearch (optional): when true, also searches the player's inventory (item-based mode only).
exports.MrNewbVehicleKeys:RemoveKeysByPlate(source, "PLATE123")
exports.MrNewbVehicleKeys:RemoveKeysByPlate(source, "PLATE123", true) -- deep search
```

### UpdateKey

```lua
-- Updates a player's key after a vehicle plate change.
-- Use this when a vehicle's plate is changed to keep the key valid.
exports.MrNewbVehicleKeys:UpdateKey(source, "OLDPLATE", "NEWPLATE")
```

### TransferKey

```lua
-- Transfers a vehicle key from one player to another.
-- The source player loses the key; the target player receives it.
exports.MrNewbVehicleKeys:TransferKey(source, targetSource, "PLATE123")
```

### DuplicateKey

```lua
-- Duplicates a vehicle key — source player retains their key and target player also receives one.
exports.MrNewbVehicleKeys:DuplicateKey(source, targetSource, "PLATE123")
```

### GetVehicleKeyList

```lua
-- Returns a table of all vehicle plates a player has keys for (alias for GetPlayerKeys).
local keys = exports.MrNewbVehicleKeys:GetVehicleKeyList(source)
```

---

## Vehicle Lock Control

### SetVehicleLock

```lua
-- Sets the lock status of a vehicle.
-- lockStatus: 1 = unlocked, 2 = locked
local netId = NetworkGetNetworkIdFromEntity(vehicle)
exports.MrNewbVehicleKeys:SetVehicleLock(netId, 2) -- lock
exports.MrNewbVehicleKeys:SetVehicleLock(netId, 1) -- unlock
```

### RemoteLock

```lua
-- Locks or unlocks a vehicle remotely by plate (does not require the vehicle to be spawned).
-- lockStatus: 1 = unlock, 2 = lock
exports.MrNewbVehicleKeys:RemoteLock(source, "PLATE123", 2) -- lock
exports.MrNewbVehicleKeys:RemoteLock(source, "PLATE123", 1) -- unlock
```

### DisableLockpickingVehicle

```lua
-- Enables or disables lockpick immunity on a vehicle.
-- status: true to prevent lockpicking, false to allow it
local netId = NetworkGetNetworkIdFromEntity(vehicle)
exports.MrNewbVehicleKeys:DisableLockpickingVehicle(netId, true)
```

---

## Ownership & Vehicle Info

### VerifyOwnership

```lua
-- Returns true if the player is the registered owner of the vehicle.
local isOwner = exports.MrNewbVehicleKeys:VerifyOwnership(source, "PLATE123")
print(isOwner) -- boolean
```

### GetVehicleInfo

```lua
-- Returns a table of stored vehicle information for the given plate, or nil if not found.
local info = exports.MrNewbVehicleKeys:GetVehicleInfo("PLATE123")
if info then
    print(info.owner) -- owner citizenid / identifier
end
```

---

## Rental System

### GrantRental

```lua
-- Grants rental access to a player for a vehicle.
-- netid is optional — pass it if the vehicle is already spawned.
exports.MrNewbVehicleKeys:GrantRental(source, "PLATE123", "adder")
exports.MrNewbVehicleKeys:GrantRental(source, "PLATE123", "adder", netId)
```

### RemoveRental

```lua
-- Removes rental access from a player for a vehicle.
-- netid is optional.
exports.MrNewbVehicleKeys:RemoveRental(source, "PLATE123")
exports.MrNewbVehicleKeys:RemoveRental(source, "PLATE123", netId)
```

---

## Temporary Keys

Temporary keys grant time-limited key access to players without permanently adding them to a vehicle's key list. Useful for timed rentals, job dispatches, or event vehicles.

### SetTempKey

```lua
-- Grants a temporary key to a player for a vehicle.
-- durationMs (optional): duration in milliseconds. Omit or pass nil for no expiry.
exports.MrNewbVehicleKeys:SetTempKey(source, "PLATE123", 300000) -- 5 minutes
exports.MrNewbVehicleKeys:SetTempKey(source, "PLATE123")         -- no expiry
```

### RemoveTempKey

```lua
-- Removes a temporary key from a player for a vehicle.
exports.MrNewbVehicleKeys:RemoveTempKey(source, "PLATE123")
```

### SetTempKeyForPlayers

```lua
-- Grants a temporary key to multiple players at once.
-- players: table of player source IDs
-- Returns the number of successful grants.
local players = { 1, 2, 3 }
exports.MrNewbVehicleKeys:SetTempKeyForPlayers(players, "PLATE123", 300000)
```

### RemoveTempKeyForPlayers

```lua
-- Removes a temporary key from multiple players at once.
-- Returns the number of successful removals.
local players = { 1, 2, 3 }
exports.MrNewbVehicleKeys:RemoveTempKeyForPlayers(players, "PLATE123")
```

### SetTempKeyForJob

```lua
-- Grants a temporary key to all currently online players with the specified job.
-- Returns the number of successful grants.
exports.MrNewbVehicleKeys:SetTempKeyForJob("police", "PLATE123", 600000) -- 10 minutes
exports.MrNewbVehicleKeys:SetTempKeyForJob("police", "PLATE123")         -- no expiry
```

### RemoveTempKeyForJob

```lua
-- Removes a temporary key from all currently online players with the specified job.
-- Returns the number of successful removals.
exports.MrNewbVehicleKeys:RemoveTempKeyForJob("police", "PLATE123")
```

---

## System Info

### KeyType

```lua
-- Returns true if the server is running in item-based key mode, false for non-item mode.
local isItemBased = exports.MrNewbVehicleKeys:KeyType()
print(isItemBased) -- boolean
```

### GetKeySystem

```lua
-- Returns the internal ServerKeySystem instance for direct method access.
-- Returns false if the system is not initialised.
local keySystem = exports.MrNewbVehicleKeys:GetKeySystem()
```

