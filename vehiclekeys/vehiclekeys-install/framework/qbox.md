---
description: >-
  To install MrNewbVehicleKeys to the core you will need use this snippet, This
  will need to be adjusted in any third party admin menus in a similar method.
icon: poop
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
// Find This in qbx_core/config/client.lua aprox around line 80

    --- Only used by QB bridge
    hasKeys = function(plate, vehicle)
        return exports.qbx_vehiclekeys:HasKeys(vehicle)
    end,
```

```lua
// Replace with this

    --- Only used by QB bridge
    hasKeys = function(plate, vehicle)
        if DoesEntityExist(vehicle) then return exports.MrNewbVehicleKeys:HaveKeys(vehicle) end
        return false
    end,
```

***

```
Step #3 adding RemoveKeys for /dv, find the below in qbx_core/server/commands.lua
```

```
// Find this

lib.addCommand('dv', {
    help = locale('command.dv.help'),
    params = {
        { name = locale('command.dv.params.radius.name'), help = locale('command.dv.params.radius.help'), type = 'number', optional = true }
    },
    restricted = 'group.admin'
}, function(source, args)
    local ped = GetPlayerPed(source)
    local pedCars = {GetVehiclePedIsIn(ped, false)}
    local radius = args[locale('command.dv.params.radius.name')]

    if pedCars[1] == 0 or radius then -- Only execute when player is not in a vehicle or radius is explicitly defined
        pedCars = lib.callback.await('qbx_core:client:getVehiclesInRadius', source, radius)
    else
        pedCars[1] = NetworkGetNetworkIdFromEntity(pedCars[1])
    end

    if #pedCars ~= 0 then
        for i = 1, #pedCars do
            local pedCar = NetworkGetEntityFromNetworkId(pedCars[i])
            if pedCar and DoesEntityExist(pedCar) then
                DeleteVehicle(pedCar)
            end
        end
    end
end)
```

```
// Replace with this

lib.addCommand('dv', {
    help = locale('command.dv.help'),
    params = {
        { name = locale('command.dv.params.radius.name'), help = locale('command.dv.params.radius.help'), type = 'number', optional = true }
    },
    restricted = 'group.admin'
}, function(source, args)
    local ped = GetPlayerPed(source)
    local pedCars = {GetVehiclePedIsIn(ped, false)}
    local radius = args[locale('command.dv.params.radius.name')]

    if pedCars[1] == 0 or radius then -- Only execute when player is not in a vehicle or radius is explicitly defined
        pedCars = lib.callback.await('qbx_core:client:getVehiclesInRadius', source, radius)
    else
        pedCars[1] = NetworkGetNetworkIdFromEntity(pedCars[1])
    end

    if #pedCars ~= 0 then
        for i = 1, #pedCars do
            local pedCar = NetworkGetEntityFromNetworkId(pedCars[i])
            if pedCar and DoesEntityExist(pedCar) then
                local plate = GetVehicleNumberPlateText(pedCar)
                exports.MrNewbVehicleKeys:RemoveKeysByPlate(source, plate)
                DeleteVehicle(pedCar)
            end
        end
    end
end)

```

Please note, if you are using an alternative admin menu that registers the command /car or dv you will need to add my exports there as well.
