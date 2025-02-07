---
description: >-
  This export will return a string with the path of the inventorys image
  location.
---

# Inventory.GetItemInfo

```lua
Bridge.Inventory.GetItemInfo(item)
```

EXAMPLE USAGE

```lua
local Bridge = exports.community_bridge:Bridge()

local itemInfo = Bridge.Inventory.GetItemInfo("water_bottle")
print(itemInfo) -- returns a table of item info. ie name/stack/label/description/image/weight etc
```

