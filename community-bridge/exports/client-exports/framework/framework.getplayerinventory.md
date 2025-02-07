---
description: This will return a table based on the framework inventory
---

# Framework.GetPlayerInventory

```
local Bridge = exports.community_bridge:Bridge()

local playerinventory = Bridge.Framework.GetPlayerInventory()
print(json.encode(playerinventory, {indent = true})
```
