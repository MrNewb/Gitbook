---
description: Add this to qb-core/shared/items.lua
icon: faucet-drip
---

# qb-core



```lua
--Old qb format
['tracker']		= {['name'] = 'tracker', 	['label'] = 'tracker',	['weight'] = 200,	['type'] = 'item',	['image'] = 'tracker.png',	['unique'] = true,	['useable'] = true,	['shouldClose'] = true,	['combinable'] = nil,	['description'] = 'Property Of LSPD'},

--New qb format

tracker		= {name = 'tracker',	        label = 'tracker',	weight = 200,         	type = 'item',         	image = 'tracker.png',			unique = true,  useable = true, shouldClose = true,   combinable = nil,   description = 'Property Of LSPD'},
```
