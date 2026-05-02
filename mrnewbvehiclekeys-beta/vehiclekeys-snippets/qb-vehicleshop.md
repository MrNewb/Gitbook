---
description: Snippet example use case in vehicleshop.
icon: car
---

# qb-vehicleshop

{% hint style="info" %}
Three events in qb-vehicleshop need key exports: giving keys on test drive start, removing them when the timer expires, and removing them if the player ends the test drive early via menu. Keys are also given on vehicle purchase.
{% endhint %}

## What This Covers

This page covers the two places that usually matter in dealership flows:

1. Temporary keys for test drives.
2. Permanent keys when the player buys the vehicle.

{% hint style="warning" %}
If your vehicleshop has extra return, cancel, preview, or cleanup paths, make sure those paths also remove keys where appropriate.
{% endhint %}

## Test Drives

The commented-out lines show the old qb-vehiclekeys events they replace.

```lua
-- Giving Keys For Test Drive
RegisterNetEvent('qb-vehicleshop:client:TestDrive', function()
    if not inTestDrive and ClosestVehicle ~= 0 then
        inTestDrive = true
        local prevCoords = GetEntityCoords(PlayerPedId())
        tempShop = insideShop
        QBCore.Functions.TriggerCallback('QBCore:Server:SpawnVehicle', function(netId)
            local veh = NetToVeh(netId)
            exports['LegacyFuel']:SetFuel(veh, 100)
            SetVehicleNumberPlateText(veh, 'TESTDRIVE')
            SetEntityHeading(veh, Config.Shops[tempShop]['TestDriveSpawn'].w)
            --TriggerEvent('vehiclekeys:client:SetOwner', QBCore.Functions.GetPlate(veh)) -- old event
            exports.MrNewbVehicleKeys:GiveKeys(veh)
            testDriveVeh = netId
            QBCore.Functions.Notify(Lang:t('general.testdrive_timenoti', { testdrivetime = Config.Shops[tempShop]['TestDriveTimeLimit'] }))
        end, Config.Shops[tempShop]['ShowroomVehicles'][ClosestVehicle].chosenVehicle, Config.Shops[tempShop]['TestDriveSpawn'], true)
        createTestDriveReturn()
        startTestDriveTimer(Config.Shops[tempShop]['TestDriveTimeLimit'] * 60, prevCoords)
    else
        QBCore.Functions.Notify(Lang:t('error.testdrive_alreadyin'), 'error')
    end
end)


-- Removing Keys when the test drive timer runs out or player leaves the vehicle
local function startTestDriveTimer(testDriveTime, prevCoords)
    local gameTimer = GetGameTimer()
    CreateThread(function()
        Wait(2000)
        while inTestDrive do
            if GetGameTimer() < gameTimer + tonumber(1000 * testDriveTime) then
                local secondsLeft = GetGameTimer() - gameTimer
                if secondsLeft >= tonumber(1000 * testDriveTime) - 20 or GetPedInVehicleSeat(NetToVeh(testDriveVeh), -1) ~= PlayerPedId() then
                    exports.MrNewbVehicleKeys:RemoveKeys(NetworkGetEntityFromNetworkId(testDriveVeh))
                    TriggerServerEvent('qb-vehicleshop:server:deleteVehicle', testDriveVeh)
                    testDriveVeh = 0
                    inTestDrive = false
                    SetEntityCoords(PlayerPedId(), prevCoords)
                    QBCore.Functions.Notify(Lang:t('general.testdrive_complete'))
                end
                drawTxt(Lang:t('general.testdrive_timer') .. math.ceil(testDriveTime - secondsLeft / 1000), 4, 0.5, 0.93, 0.50, 255, 255, 255, 180)
            end
            Wait(0)
        end
    end)
end

-- Removing Keys when the player ends the test drive early via menu
RegisterNetEvent('qb-vehicleshop:client:TestDriveReturn', function()
    local ped = PlayerPedId()
    local veh = GetVehiclePedIsIn(ped)
    local entity = NetworkGetEntityFromNetworkId(testDriveVeh)
    if veh == entity then
        exports.MrNewbVehicleKeys:RemoveKeys(entity)
        testDriveVeh = 0
        inTestDrive = false
        DeleteEntity(veh)
        exports['qb-menu']:closeMenu()
        testDriveZone:destroy()
    else
        QBCore.Functions.Notify(Lang:t('error.testdrive_return'), 'error')
    end
end)
```

## Purchase Car

```lua
RegisterNetEvent('qb-vehicleshop:client:buyShowroomVehicle', function(vehicle, plate)
    tempShop = insideShop
    QBCore.Functions.TriggerCallback('QBCore:Server:SpawnVehicle', function(netId)
        local veh = NetToVeh(netId)
        exports['LegacyFuel']:SetFuel(veh, 100)
        SetVehicleNumberPlateText(veh, plate)
        SetEntityHeading(veh, Config.Shops[tempShop]['VehicleSpawn'].w)
        --TriggerEvent('vehiclekeys:client:SetOwner', QBCore.Functions.GetPlate(veh)) -- old event
        exports.MrNewbVehicleKeys:GiveKeys(veh)
        TriggerServerEvent('qb-mechanicjob:server:SaveVehicleProps', QBCore.Functions.GetVehicleProperties(veh))
    end, vehicle, Config.Shops[tempShop]['VehicleSpawn'], true)
end)
```

{% hint style="success" %}
After patching, test both success and cleanup flows: start a test drive, let it expire, end one early, and then buy a vehicle to confirm each path grants or removes keys correctly.
{% endhint %}
