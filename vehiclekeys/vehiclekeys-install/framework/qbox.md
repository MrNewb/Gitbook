---
icon: poop
description: >-
  To install MrNewbVehicleKeys to the core you will need use this snippet, This
  will need to be adjusted in any third party admin menus in a similar method.
---

# qbox

```
Step #1 GiveKeys
```

```lua
-- Find This in qbx_core/config/server.lua aprox around line 114

    giveVehicleKeys = function(src, plate, vehicle)
        return exports.qbx_vehiclekeys:GiveKeys(src, vehicle)
    end,
```

```lua
-- Paste this in in its place

    giveVehicleKeys = function(src, plate, vehicle)
        local netId = NetworkGetNetworkIdFromEntity(vehicle)
        return exports.MrNewbVehicleKeys:GiveKeys(src, netId)
    end,
```

***

```
Step #2 hasKeys
```

```lua
-- Find This in qbx_core/config/client.lua aprox around line 80

    --- Only used by QB bridge
    hasKeys = function(plate, vehicle)
        return exports.qbx_vehiclekeys:HasKeys(vehicle)
    end,
```

```lua
-- Paste this in in its place

    --- Only used by QB bridge
    hasKeys = function(plate, vehicle)
        if DoesEntityExist(vehicle) then return exports.MrNewbVehicleKeys:HaveKeys(vehicle) end
        return false
    end,
```



Please note, if you are using an alternative admin menu that registers the command /car you will need to add my exports there as well.
