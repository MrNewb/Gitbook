---
description: Snippet example use case in garages.
icon: garage
---

# qb-garages

Here is a client side example on the usage of my exports in the script.

## Granting Keys

```lua
RegisterNetEvent('qb-garages:client:takeOutGarage', function(data)
    QBCore.Functions.TriggerCallback('qb-garages:server:IsSpawnOk', function(spawn)
        if spawn then
            local location = GetSpawnPoint(data.garage)
            if not location then return end
            QBCore.Functions.TriggerCallback('qb-garages:server:spawnvehicle', function(netId, properties, vehPlate)
                while not NetworkDoesNetworkIdExist(netId) do Wait(10) end
                local veh = NetworkGetEntityFromNetworkId(netId)
                Citizen.Await(CheckPlate(veh, vehPlate))
                QBCore.Functions.SetVehicleProperties(veh, properties)
                exports[Config.FuelResource]:SetFuel(veh, data.stats.fuel)
                TriggerServerEvent('qb-garages:server:updateVehicleState', 0, vehPlate)
                --TriggerEvent('vehiclekeys:client:SetOwner', vehPlate)
                exports.MrNewbVehicleKeys:GiveKeys(veh) -- add this here
                if Config.Warp then TaskWarpPedIntoVehicle(PlayerPedId(), veh, -1) end
                if Config.VisuallyDamageCars then doCarDamage(veh, data.stats, properties) end
                SetVehicleEngineOn(veh, true, true, false)
            end, data.plate, data.vehicle, location, true)
        else
            QBCore.Functions.Notify(Lang:t('error.not_depot'), 'error', 5000)
        end
    end, data.plate, data.type)
end)
```

In the above example I left in the commented out code so you can see the similar option below it.



## Removing Keys

```lua
local function CheckPlayers(vehicle)
    for i = -1, 5, 1 do
        local seat = GetPedInVehicleSeat(vehicle, i)
        if seat then
            TaskLeaveVehicle(seat, vehicle, 0)
        end
    end
    exports.MrNewbVehicleKeys:RemoveKeys(vehicle) -- Add this here
    Wait(1500)
    QBCore.Functions.DeleteVehicle(vehicle)
end
```

