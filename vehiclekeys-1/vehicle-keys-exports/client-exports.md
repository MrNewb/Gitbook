---
description: This is a list of the available client side exports.
---

# Client Exports

## Key Management

### HasVehicleKeys

```lua
-- Returns true if the local player has keys to the given vehicle entity.
-- vehicle: vehicle entity handle
local hasKeys = exports.MrNewbVehicleKeys:HasVehicleKeys(vehicle)
print(hasKeys) -- boolean
```

### HaveKeys

```lua
-- Alias for HasVehicleKeys.
local hasKeys = exports.MrNewbVehicleKeys:HaveKeys(vehicle)
print(hasKeys) -- boolean
```

### HasKeysByPlate

```lua
-- Returns true if the local player has keys for a vehicle with the given plate.
local hasKeys = exports.MrNewbVehicleKeys:HasKeysByPlate("PLATE123")
print(hasKeys) -- boolean
```

### GiveKeys

```lua
-- Gives the local player keys to a vehicle by entity.
-- vehicle: vehicle entity handle
exports.MrNewbVehicleKeys:GiveKeys(vehicle)
```

### GiveKeysByPlate

```lua
-- Gives the local player keys to a vehicle by plate string.
exports.MrNewbVehicleKeys:GiveKeysByPlate("PLATE123")
```

### RemoveKeys

```lua
-- Removes the local player's keys to a vehicle by entity.
-- vehicle: vehicle entity handle
exports.MrNewbVehicleKeys:RemoveKeys(vehicle)
```

### RemoveKeysByPlate

```lua
-- Removes the local player's keys to a vehicle by plate string.
exports.MrNewbVehicleKeys:RemoveKeysByPlate("PLATE123")
```

### GetPlayerKeyList

```lua
-- Returns a table of all plates the local player currently has keys for.
local keys = exports.MrNewbVehicleKeys:GetPlayerKeyList()
for _, plate in ipairs(keys) do
    print(plate)
end
```

### GetVehicleState

```lua
-- Returns true if the local player has keys to their current vehicle
-- or the closest vehicle within 10 metres.
local hasKeys = exports.MrNewbVehicleKeys:GetVehicleState()
print(hasKeys) -- boolean
```

---

## Engine Control

### ToggleEngine

```lua
-- Toggles the engine of a vehicle on or off.
-- forceState (optional): pass true to force on, false to force off, nil to toggle.
exports.MrNewbVehicleKeys:ToggleEngine(vehicle)
exports.MrNewbVehicleKeys:ToggleEngine(vehicle, true)  -- force on
exports.MrNewbVehicleKeys:ToggleEngine(vehicle, false) -- force off
```

---

## Lock Control

### ToggleLock

```lua
-- Toggles the door lock on a vehicle.
-- vehicle: vehicle entity handle
exports.MrNewbVehicleKeys:ToggleLock(vehicle)
```

---

## Hotwire Status & Control

### IsVehicleHotwired

```lua
-- Returns true if the vehicle has been hotwired.
local hotwired = exports.MrNewbVehicleKeys:IsVehicleHotwired(vehicle)
print(hotwired) -- boolean
```

### CheckIfHotwired

```lua
-- Alias for IsVehicleHotwired.
local hotwired = exports.MrNewbVehicleKeys:CheckIfHotwired(vehicle)
```

### GetHotWiredStatus

```lua
-- Alias for IsVehicleHotwired.
local hotwired = exports.MrNewbVehicleKeys:GetHotWiredStatus(vehicle)
```

### SetVehicleHotwireImmune

```lua
-- Makes a vehicle immune to hotwiring (or removes immunity).
-- immune: true to prevent hotwiring, false to allow it
exports.MrNewbVehicleKeys:SetVehicleHotwireImmune(vehicle, true)
```

---

## Lockpick Protection

### SetVehicleLockpickImmuneEntity

```lua
-- Makes a vehicle immune to lockpicking by entity handle.
-- immune: true to prevent lockpicking, false to allow it
exports.MrNewbVehicleKeys:SetVehicleLockpickImmuneEntity(vehicle, true)
```

### SetVehicleLockpickImmunePlate

```lua
-- Makes a vehicle immune to lockpicking by plate string.
-- immune: true to prevent lockpicking, false to allow it
exports.MrNewbVehicleKeys:SetVehicleLockpickImmunePlate("PLATE123", true)
```

---

## Temporary Keys

Temporary keys allow time-limited or bypass access to vehicles without permanent key ownership. Useful for vehicle shops, test drives, and similar scenarios.

### GetTempKey

```lua
-- Returns the current global temporary key bypass state (true = enabled).
local enabled = exports.MrNewbVehicleKeys:GetTempKey()
print(enabled) -- boolean
```

### SetTempKey

```lua
-- Sets the global temporary key bypass state.
-- When true, the player can access any vehicle without needing keys.
-- Useful during vehicle shop previews — enable on entry, disable on exit.
exports.MrNewbVehicleKeys:SetTempKey(true)
exports.MrNewbVehicleKeys:SetTempKey(false)
```

### ToggleTempKey

```lua
-- Alias for SetTempKey.
exports.MrNewbVehicleKeys:ToggleTempKey(true)
exports.MrNewbVehicleKeys:ToggleTempKey(false)
```

### SetTempKeyByPlate

```lua
-- Grants a temporary key for a specific vehicle by plate.
-- durationMs (optional): duration in milliseconds. Omit for a permanent temp key.
exports.MrNewbVehicleKeys:SetTempKeyByPlate("PLATE123", 60000) -- 60 seconds
exports.MrNewbVehicleKeys:SetTempKeyByPlate("PLATE123")        -- no expiry
```

### HasTempKey

```lua
-- Returns true if the player has a valid (non-expired) temporary key for the plate.
local hasTempKey = exports.MrNewbVehicleKeys:HasTempKey("PLATE123")
print(hasTempKey) -- boolean
```

### RemoveTempKeyByPlate

```lua
-- Removes a temporary key for a specific vehicle by plate.
exports.MrNewbVehicleKeys:RemoveTempKeyByPlate("PLATE123")
```

---

## Vehicle Access & Requirements

### DoesVehicleRequireKey

```lua
-- Returns true if the vehicle is subject to the key system
-- (i.e. it is not on the blacklisted/exempt vehicle list).
local requiresKey = exports.MrNewbVehicleKeys:DoesVehicleRequireKey(vehicle)
print(requiresKey) -- boolean
```

### IsSharedJobVehicle

```lua
-- Returns true if the vehicle is accessible to the player through their job.
local isJobVehicle = exports.MrNewbVehicleKeys:IsSharedJobVehicle(vehicle)
print(isJobVehicle) -- boolean
```

### CheckForJobVehicle

```lua
-- Alias for IsSharedJobVehicle.
local isJobVehicle = exports.MrNewbVehicleKeys:CheckForJobVehicle(vehicle)
```

### CheckVehicleAccess

```lua
-- Performs a full access check on a vehicle, enforcing any access restrictions.
-- Uses the player's current vehicle if no entity is passed.
local canAccess = exports.MrNewbVehicleKeys:CheckVehicleAccess(vehicle)
print(canAccess) -- boolean
```

---

## Keyfob & Advanced Actions

### OpenKeyFob

```lua
-- Opens the keyfob UI for a vehicle.
-- plate:   vehicle plate string
-- buttons: table of button action IDs to display (see Config.Buttons)
exports.MrNewbVehicleKeys:OpenKeyFob("PLATE123", { "lock", "unlock", "trunk" })
```

### StartVehicleAlarm

```lua
-- Triggers the vehicle alarm.
exports.MrNewbVehicleKeys:StartVehicleAlarm(vehicle)
```

### ToggleTrunk

```lua
-- Toggles the vehicle trunk open or closed.
exports.MrNewbVehicleKeys:ToggleTrunk(vehicle)
```

### ToggleRemoteStart

```lua
-- Remotely starts the vehicle engine from a distance.
exports.MrNewbVehicleKeys:ToggleRemoteStart(vehicle)
```

### DanceMode

```lua
-- Activates dance mode: honks the horn, flashes lights, and pulses the doors.
exports.MrNewbVehicleKeys:DanceMode(vehicle)
```

### SelfParkVehicle

```lua
-- Parks the vehicle at the nearest configured parking spot.
-- Returns the parked coordinates (vector3) on success, or false on failure.
local coords = exports.MrNewbVehicleKeys:SelfParkVehicle(vehicle)
```

### SummonVehicle

```lua
-- Drives the vehicle to the player's current location.
exports.MrNewbVehicleKeys:SummonVehicle(vehicle)
```

### ToggleAutoPilot

```lua
-- Enables auto-pilot, driving the vehicle to the current GPS destination.
exports.MrNewbVehicleKeys:ToggleAutoPilot(vehicle)
```

---

## System Info

### GetKeySystem

```lua
-- Returns the internal ClientKeySystem object for direct method calls.
-- Returns false if the system is not initialised.
local keySystem = exports.MrNewbVehicleKeys:GetKeySystem()
```
