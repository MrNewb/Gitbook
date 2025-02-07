---
description: >-
  This export will return a string with the path of the inventorys image
  location.
---

# Inventory.GetImagePath

```lua
Bridge.Inventory.GetImagePath(item)
```

EXAMPLE USAGE

```lua
local Bridge = exports.community_bridge:Bridge()

local myImagePath = Bridge.Inventory.GetImagePath("water_bottle")
print(myImagePath) -- nui://codem-inventory/html/images/water_bottle.png
print(myImagePath) -- nui://ox_inventory/web/images/water_bottle.png
```

