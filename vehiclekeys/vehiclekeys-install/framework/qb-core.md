---
icon: faucet-drip
description: To install MrNewbVehicleKeys to the core you will need use this snippet
---

# qb-core

```
Step #1 GiveKeys
```

```lua
-- Find This in qb-core/client/events.lua aprox around line 121

RegisterNetEvent('QBCore:Command:SpawnVehicle', function(vehName)
    local ped = PlayerPedId()
    local hash = joaat(vehName)
    local veh = GetVehiclePedIsUsing(ped)
    if not IsModelInCdimage(hash) then return end
    RequestModel(hash)
    while not HasModelLoaded(hash) do
        Wait(0)
    end

    if IsPedInAnyVehicle(ped) then
        SetEntityAsMissionEntity(veh, true, true)
        DeleteVehicle(veh)
    end

    local vehicle = CreateVehicle(hash, GetEntityCoords(ped), GetEntityHeading(ped), true, false)
    TaskWarpPedIntoVehicle(ped, vehicle, -1)
    SetVehicleFuelLevel(vehicle, 100.0)
    SetVehicleDirtLevel(vehicle, 0.0)
    SetModelAsNoLongerNeeded(hash)
    TriggerEvent('vehiclekeys:client:SetOwner', QBCore.Functions.GetPlate(vehicle))
end)
```

```lua
-- Paste this in in its place

RegisterNetEvent('QBCore:Command:SpawnVehicle', function(vehName)
    local ped = PlayerPedId()
    local hash = joaat(vehName)
    local veh = GetVehiclePedIsUsing(ped)
    if not IsModelInCdimage(hash) then return end
    RequestModel(hash)
    while not HasModelLoaded(hash) do
        Wait(0)
    end

    if IsPedInAnyVehicle(ped) then
        SetEntityAsMissionEntity(veh, true, true)
        DeleteVehicle(veh)
    end

    local vehicle = CreateVehicle(hash, GetEntityCoords(ped), GetEntityHeading(ped), true, false)
    TaskWarpPedIntoVehicle(ped, vehicle, -1)
    SetVehicleFuelLevel(vehicle, 100.0)
    SetVehicleDirtLevel(vehicle, 0.0)
    SetModelAsNoLongerNeeded(hash)
    --TriggerEvent('vehiclekeys:client:SetOwner', QBCore.Functions.GetPlate(vehicle))
    exports.MrNewbVehicleKeys:GiveKeys(vehicle)
end)
```

***



```
Step #2 RemoveKeys for /dv
```

```lua
-- Find This in qb-core/client/events.lua aprox around line 144

RegisterNetEvent('QBCore:Command:DeleteVehicle', function()
    local ped = PlayerPedId()
    local veh = GetVehiclePedIsUsing(ped)
    if veh ~= 0 then
        SetEntityAsMissionEntity(veh, true, true)
        DeleteVehicle(veh)
    else
        local pcoords = GetEntityCoords(ped)
        local vehicles = GetGamePool('CVehicle')
        for _, v in pairs(vehicles) do
            if #(pcoords - GetEntityCoords(v)) <= 5.0 then
                SetEntityAsMissionEntity(v, true, true)
                DeleteVehicle(v)
            end
        end
    end
end)
```

```
-- Paste this in in its place
```

```lua
-- Paste this in in its place

RegisterNetEvent('QBCore:Command:DeleteVehicle', function()
    local ped = PlayerPedId()
    local veh = GetVehiclePedIsUsing(ped)
    if veh ~= 0 then
        exports.MrNewbVehicleKeys:RemoveKeys(veh)
        SetEntityAsMissionEntity(veh, true, true)
        DeleteVehicle(veh)
    else
        local pcoords = GetEntityCoords(ped)
        local vehicles = GetGamePool('CVehicle')
        for _, v in pairs(vehicles) do
            if #(pcoords - GetEntityCoords(v)) <= 5.0 then
                exports.MrNewbVehicleKeys:RemoveKeys(v)
                SetEntityAsMissionEntity(v, true, true)
                DeleteVehicle(v)
            end
        end
    end
end)

```

***

```
Step #3 Go to qb-core/shared/items.lua and paste this in, depending on the qb
version you use I have added both qbs old and new formats
```

```lua
['vehiclekeys'] 		= {['name'] = 'vehiclekeys', 			['label'] = 'Vehicle Keys', 			['weight'] = 100, ['type'] = 'item', ['image'] = 'vehiclekeys.png', 		['unique'] = true, 	['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'Fancy vehicle keys'},
['keyring'] 			= {['name'] = 'keyring', 			['label'] = 'Keyring', 				['weight'] = 220, ['type'] = 'item', ['image'] = 'keyring.png', 		['unique'] = false,     ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'A keyring that holds car keys.'},
['aftermarket_locks'] 	        = {['name'] = 'aftermarket_locks', 		['label'] = 'Aftermarket Lock System',          ['weight'] = 220, ['type'] = 'item', ['image'] = 'aftermarket_locks.png', 	['unique'] = false,     ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'A Vehicle Lock System To Replace Key Systems'},
['lockpick'] 			= {['name'] = 'lockpick', 			['label'] = 'Lockpick', 		 	['weight'] = 850, ['type'] = 'item', ['image'] = 'lockpick.png', 		['unique'] = false,     ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'A mysterious device.'},
['advancedlockpick'] 	        = {['name'] = 'advancedlockpick', 		['label'] = 'Advanced Lockpick', 		['weight'] = 850, ['type'] = 'item', ['image'] = 'advancedlockpick.png', 	['unique'] = false,     ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'A upgraded mysterious device.'},




vehiclekeys                  = { name = 'vehiclekeys',              label = 'Vehicle Keys',             weight = 100, type = 'item', image = 'vehiclekeys.png',         unique = true,     useable = true, shouldClose = true, combinable = nil, description = 'Fancy vehicle keys' },
keyring                      = { name = 'keyring',                  label = 'Vehicle Key Ring',         weight = 100, type = 'item', image = 'keyring.png',             unique = true,     useable = true, shouldClose = true, combinable = nil, description = 'A keyring to solve all problems.' },
aftermarket_locks            = { name = 'aftermarket_locks',        label = 'Aftermarket Lock System',  weight = 100, type = 'item', image = 'aftermarket_locks.png',   unique = true,     useable = true, shouldClose = true, combinable = nil, description = 'A Vehicle Lock System To Replace Key Systems' },
lockpick                     = { name = 'lockpick',                 label = 'Lockpick',                 weight = 300, type = 'item', image = 'lockpick.png',            unique = false,    useable = true, shouldClose = true, combinable = nil, description = 'A mysterious device.' },
advancedlockpick             = { name = 'advancedlockpick',         label = 'Advanced Lockpick',        weight = 500, type = 'item', image = 'advancedlockpick.png',    unique = false,    useable = true, shouldClose = true, combinable = nil, description = 'A upgraded mysterious device.' },

```

Please note, if you are using an alternative admin menu that registers the command /car you will need to add my exports there as well.
