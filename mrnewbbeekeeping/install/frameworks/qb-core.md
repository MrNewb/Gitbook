---
description: Add this to qb-core/shared/items.lua
icon: faucet-drip
---

# qb-core



```lua
    -- Newer qb format
    beehive                      = { name = 'beehive',      label = 'Beehive',          weight = 100,   type = 'item',  image = 'beehive.png',      unique = true,      useable = true,     shouldClose = true,     description = 'A Beehive' },
    queen_bee                    = { name = 'queen_bee',    label = 'Queen Bee',        weight = 100,   type = 'item',  image = 'queen_bee.png',    unique = false,     useable = true,     shouldClose = true,     description = 'Queen Bee' },
    worker_bees                  = { name = 'worker_bees',  label = 'Worker Bees',      weight = 100,   type = 'item',  image = 'worker_bees.png',  unique = false,     useable = true,     shouldClose = true,     description = 'Worker Bees' },
    bees_wax                     = { name = 'bees_wax',     label = 'Bees Wax',         weight = 100,   type = 'item',  image = 'bees_wax.png',     unique = false,     useable = true,     shouldClose = true,     description = 'Bees Wax' },
    red_honey                    = { name = 'red_honey',    label = 'Red Bees Honey',   weight = 100,   type = 'item',  image = 'red_honey.png',    unique = false,     useable = true,     shouldClose = true,     description = 'Red Bees Honey' },
    green_honey                  = { name = 'green_honey',  label = 'Green Bees Honey', weight = 100,   type = 'item',  image = 'green_honey.png',  unique = false,     useable = true,     shouldClose = true,     description = 'Green Bees Honey' },
    blue_honey                   = { name = 'blue_honey',   label = 'Blue Bees Honey',  weight = 100,   type = 'item',  image = 'blue_honey.png',   unique = false,     useable = true,     shouldClose = true,     description = 'Blue Bees Honey' },
    bees_honey                   = { name = 'bees_honey',   label = 'Bees Honey',       weight = 100,   type = 'item',  image = 'bees_honey.png',   unique = false,     useable = true,     shouldClose = true,     description = 'Bees Honey' },


    -- Older qb format
    ["beehive"]                 = {['name'] = "beehive",            ['label'] = "Beehive",              ['weight'] = 2000,      ['type'] = "item",          ['image'] = "beehive.png",          ['unique'] = false,     ['useable'] = true,     ['shouldClose'] = true,     ['combinable'] = nil,       ['description'] = "Beehive" },
    ["queen_bee"]               = {['name'] = "queen_bee",          ['label'] = "Queen Bee",            ['weight'] = 10,        ['type'] = "item",          ['image'] = "queen_bee.png",        ['unique'] = false,     ['useable'] = true,     ['shouldClose'] = true,     ['combinable'] = nil,       ['description'] = "Queen Bee" },
    ["worker_bees"]             = {['name'] = "worker_bees",        ['label'] = "Worker Bees",          ['weight'] = 10,        ['type'] = "item",          ['image'] = "worker_bees.png",      ['unique'] = false,     ['useable'] = true,     ['shouldClose'] = true,     ['combinable'] = nil,       ['description'] = "Worker Bees" },
    ["bees_wax"]                = {['name'] = "bees_wax",           ['label'] = "Bees Wax",             ['weight'] = 1,         ['type']= "item",           ['image'] = "bees_wax.png",         ['unique'] = false,     ['useable'] = true,     ['shouldClose'] = true,     ['combinable'] = nil,       ['description'] = "Bees Wax" },
    ["red_honey"]               = {['name'] = "red_honey",          ['label'] = "Red Bees Honey",       ['weight'] = 1,         ['type'] = "item",          ['image'] = "red_honey.png",        ['unique'] = false,     ['useable'] = true,     ['shouldClose'] = true,     ['combinable'] = nil,       ['description'] = "Red Bees Honey" },
    ["green_honey"]             = {['name'] = "green_honey",        ['label'] = "Green Bees Honey",     ['weight'] = 1,         ['type'] = "item",          ['image'] = "green_honey.png",      ['unique'] = false,     ['useable'] = true,     ['shouldClose'] = true,     ['combinable'] = nil,       ['description'] = "Green Bees Honey" },
    ["blue_honey"]              = {['name'] = "blue_honey",         ['label'] = "Blue Bees Honey",      ['weight'] = 1,         ['type'] = "item",          ['image'] = "blue_honey.png",       ['unique'] = false,     ['useable'] = true,     ['shouldClose'] = true,     ['combinable'] = nil,       ['description'] = "Blue Bees Honey" },
    ["bees_honey"]              = {['name'] = "bees_honey",         ['label'] = "Bees Honey",           ['weight'] = 1,         ['type'] = "item",          ['image'] = "bees_honey.png",       ['unique'] = false,     ['useable'] = true,     ['shouldClose'] = true,     ['combinable'] = nil,       ['description'] = "Bees Honey" },

```
