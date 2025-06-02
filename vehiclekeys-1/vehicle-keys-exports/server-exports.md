---
description: This is a list of the available server side exports.
---

# Server Exports

```
IsPlayerWearingVest
```

```lua
-- This export will return true/false (boolean) if a player is wearing a plate carrier
local isplayerinvest = exports.MrNewbPlateCarriers:IsPlayerWearingVest(src)
if isplayerinvest then
    print("Yep")
else
    print("Nope")
end
```

```
ForceRemovePlayerVest
```

```lua
-- This export will remove a vest if a player is wearing one. Returns true
local removevest = exports.MrNewbPlateCarriers:ForceRemovePlayerVest(src)
if removevest then
    print("Yep")
else
    print("Nope")
end
```
