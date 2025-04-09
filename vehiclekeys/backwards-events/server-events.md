---
description: This is a list of the available Backwards Server side events.
---

# Server Events



```lua
qb-vehiclekeys:server:AcquireVehicleKeys
```

```lua
-- plate is a string of the vehicles plate
local plate = "platenumberhere"
TriggerServerEvent('qb-vehiclekeys:server:AcquireVehicleKeys', plate)
```

```lua
qb-vehiclekeys:server:GiveVehicleKeys
```

```lua
-- plate is a string of the vehicles plate
local plate = "platenumberhere"
TriggerServerEvent('qb-vehiclekeys:server:GiveVehicleKeys', plate)
```

