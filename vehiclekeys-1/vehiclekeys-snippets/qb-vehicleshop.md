---
description: Snippet example use case in vehicleshop.
icon: car
---

# qb-vehicleshop

Here is a client side example on the usage of my exports in the script.

## Test Drives

```lua
-- Giving Keys For Test Drive
RegisterNetEvent('qb-vehicleshop:client:TestDrive', function()
    if not inTestDrive and ClosestVehicle ~= 0 then
        inTestDrive = true
        local prevCoords = GetEntityCoords(PlayerPedId())
        tempShop = insideShop -- temp hacky way of setting the shop because it changes after the callback has returned since you are outside the zone
        QBCore.Functions.TriggerCallback('QBCore:Server:SpawnVehicle', function(netId)
            local veh = NetToVeh(netId)
            exports['LegacyFuel']:SetFuel(veh, 100)
            SetVehicleNumberPlateText(veh, 'TESTDRIVE')
            SetEntityHeading(veh, Config.Shops[tempShop]['TestDriveSpawn'].w)
            --TriggerEvent('vehiclekeys:client:SetOwner', QBCore.Functions.GetPlate(veh))
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


-- Removing Keys After Test Drives forced
local function startTestDriveTimer(testDriveTime, prevCoords)
    local gameTimer = GetGameTimer()
    CreateThread(function()
        Wait(2000) -- Avoids the condition to run before entering vehicle
        while inTestDrive do
            if GetGameTimer() < gameTimer + tonumber(1000 * testDriveTime) then
                local secondsLeft = GetGameTimer() - gameTimer
                if secondsLeft >= tonumber(1000 * testDriveTime) - 20 or GetPedInVehicleSeat(NetToVeh(testDriveVeh), -1) ~= PlayerPedId() then
                    exports.MrNewbVehicleKeys:RemoveKeys(NetworkGetEntityFromNetworkId(testDriveVeh)) -- add this
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

-- Removing Keys After Test Drives menu
RegisterNetEvent('qb-vehicleshop:client:TestDriveReturn', function()
    local ped = PlayerPedId()
    local veh = GetVehiclePedIsIn(ped)
    local entity = NetworkGetEntityFromNetworkId(testDriveVeh)
    if veh == entity then
        exports.MrNewbVehicleKeys:RemoveKeys(entity) -- add this
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

In the above example I left in the commented out code so you can see the changes it, it being commented out will not hurt anything.

## Purchase Car

```lua
RegisterNetEvent('qb-vehicleshop:client:buyShowroomVehicle', function(vehicle, plate)
    tempShop = insideShop -- temp hacky way of setting the shop because it changes after the callback has returned since you are outside the zone
    QBCore.Functions.TriggerCallback('QBCore:Server:SpawnVehicle', function(netId)
        local veh = NetToVeh(netId)
        exports['LegacyFuel']:SetFuel(veh, 100)
        SetVehicleNumberPlateText(veh, plate)
        SetEntityHeading(veh, Config.Shops[tempShop]['VehicleSpawn'].w)
        --TriggerEvent('vehiclekeys:client:SetOwner', QBCore.Functions.GetPlate(veh))
        exports.MrNewbVehicleKeys:GiveKeys(veh) -- add this
        TriggerServerEvent('qb-mechanicjob:server:SaveVehicleProps', QBCore.Functions.GetVehicleProperties(veh))
    end, vehicle, Config.Shops[tempShop]['VehicleSpawn'], true)
end)
```
