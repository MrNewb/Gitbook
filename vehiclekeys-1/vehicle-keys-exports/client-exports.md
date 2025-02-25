---
description: This is a list of the available client side exports.
---

# Client Exports

## GiveKeysByPlate

```lua
-- plate is a string of the vehicles plate
local plate = "platenumberhere"
exports.MrNewbVehicleKeys:GiveKeysByPlate(plate)
```

## GiveKeys

```lua
-- vehicle: This would be the vehicle entity

exports.MrNewbVehicleKeys:GiveKeys(vehicle)
```

## RemoveKeysByPlate

```lua
-- plate is a string of the vehicles plate
local plate = "platenumberhere"
exports.MrNewbVehicleKeys:RemoveKeysByPlate(plate)
```

## RemoveKeys

```lua
-- vehicle: This would be the vehicle entity

exports.MrNewbVehicleKeys:RemoveKeys(vehicle)
```

## GetVehicleState

<pre class="language-lua"><code class="lang-lua">-- This export will return a boolean (true/false) if you have keys to the closest vehicle
<strong>
</strong><strong>exports.MrNewbVehicleKeys:GetVehicleState()
</strong></code></pre>

## HasKeysByPlate

```lua
local plate = "platenumberhere"
local haskeys = exports.MrNewbVehicleKeys:HasKeysByPlate(plate)
print(haskeys) -- will be bool
```

## HaveKeys

```lua
-- vehicle: This would be the vehicle you want to check if the player has keys to

exports.MrNewbVehicleKeys:HaveKeys(vehicle)
```

## ToggleTempKey

```lua
-- This export will enable a bypass to the key system, it is useful for some vehicle
-- shops that warp a player into cars when using keys as an item
-- this is a toggle that you enable with true and disable with false
-- idealy when entering a menu setting to true and on exit to false

exports.MrNewbVehicleKeys:ToggleTempKey(true)
```

## GetTempKey

<pre class="language-lua"><code class="lang-lua">-- This export will truen a boolean (true/false) if the temp key export is enabled
<strong>
</strong><strong>exports.MrNewbVehicleKeys:GetTempKey()
</strong></code></pre>

## RemoveKeysByPlate

```lua
-- This export will remove a key from a player based on the plates string
-- platestring: this will be the plate of a vehicle

exports.MrNewbVehicleKeys:RemoveKeysByPlate(platestring)
```

