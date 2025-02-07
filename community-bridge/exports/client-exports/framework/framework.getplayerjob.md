---
description: This has 4 returns, job name, job label, job grade name,  job grade level
---

# Framework.GetPlayerJob

```
local Bridge = exports.community_bridge:Bridge()

local playerjobname, playerjoblabel, playerjobgradename, playerjobgradelevel = Bridge.Framework.GetPlayerJob()
print(playerjobname) -- police
print(playerjoblabel) -- Police
print(playerjobgradename) -- Lieutenant
print(playerjobgradelevel) -- 3
```
