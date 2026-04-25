---
description: Snippet example use case in garages.
icon: garage
---

# qb-garages

{% hint style="info" %}
These are the two places in qb-garages that need key exports added: when a vehicle is taken out of the garage (give keys) and when the garage deletes a vehicle (remove keys). Adapt the pattern to whichever garage script you use.
{% endhint %}

## Granting Keys on Garage Takeout

Add `exports.MrNewbVehicleKeys:GiveKeys(veh)` after the vehicle is spawned and the player is seated. The commented-out line shows the old qb-vehiclekeys event it replaces.

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
                --TriggerEvent('vehiclekeys:client:SetOwner', vehPlate) -- old event, replaced below
                exports.MrNewbVehicleKeys:GiveKeys(veh)
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

## Removing Keys on Vehicle Delete

Add `exports.MrNewbVehicleKeys:RemoveKeys(vehicle)` before the vehicle is deleted so keys are cleaned up from the player's inventory.

```lua
local function CheckPlayers(vehicle)
    for i = -1, 5, 1 do
        local seat = GetPedInVehicleSeat(vehicle, i)
        if seat then
            TaskLeaveVehicle(seat, vehicle, 0)
        end
    end
    exports.MrNewbVehicleKeys:RemoveKeys(vehicle)
    Wait(1000)
    QBCore.Functions.DeleteVehicle(vehicle)
end
```

