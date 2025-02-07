---
description: This will toggle weather sync with the server for the client
---

# Weather.ToggleSync

```
local Bridge = exports.community_bridge:Bridge()

-- Disable weather sync, you can set weather via natives after this
Bridge.Weather.ToggleSync(false)


-- Enable weather sync, you can sync the client to the weather system with the other players after this
Bridge.Weather.ToggleSync(true)
```
