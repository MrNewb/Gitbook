---
description: This is a list of the available server side exports.
---

# Server Exports

This export is optional — you can simply give the item normally if you prefer. I included it in case you want to integrate a reward function from a login reward script or something similar.

```
GiveGiftBox
```

```lua
-- Give a starter box to a player
local giftboxType = "starter_box"
exports.MrNewbGiftBox:GiveGiftBox(source, giftboxType, 1)
```
