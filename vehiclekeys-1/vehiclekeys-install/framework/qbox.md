---
description: >-
  To install MrNewbVehicleKeys to the core you will need use this snippet, This
  will need to be adjusted in any third party admin menus in a similar method.
icon: poop
---

# qbox

{% hint style="warning" %}
Remove or disable `qbx_vehiclekeys` before starting MrNewbVehicleKeys.
{% endhint %}

## Step 1 — GiveKeys hook

**Find this in `qbx_core/config/server.lua` (around line 119):**

```lua
    giveVehicleKeys = function(src, plate, vehicle)
        return exports.qbx_vehiclekeys:GiveKeys(src, vehicle)
    end,
```

**Replace with:**

```lua
giveVehicleKeys = function(src, plate, vehicle)
    -- usage of the spawnvehicle return in qb shows the second return is the entity id and not a network id, we will trust that its accurate here.
    return exports.MrNewbVehicleKeys:GiveKeys(src, vehicle)
end,
```

---

## Step 2 — setvehiclelock hook

**Find this in `qbx_core/config/server.lua` (around line 123):**

```lua
    setVehicleLock = function(vehicle, state)
        exports.qbx_vehiclekeys:SetLockState(vehicle, state)
    end,
```

**Replace with:**

```lua
    setVehicleLock = function(vehicle, state)
        --exports.qbx_vehiclekeys:SetLockState(vehicle, state)
    end,
```

---

## Step 3 — hasKeys hook

**Find this in `qbx_core/config/client.lua` (around line 80):**

```lua
--- Only used by QB bridge
hasKeys = function(plate, vehicle)
    return GetResourceState('qbx_vehiclekeys') ~= 'started' or exports.qbx_vehiclekeys:HasKeys(vehicle)
end,
```

**Replace with:**

```lua
--- Only used by QB bridge
hasKeys = function(plate, vehicle)
    if DoesEntityExist(vehicle) then return exports.MrNewbVehicleKeys:HaveKeys(vehicle) end
    return false
end,
```

---

## Step 4 — Remove keys when a vehicle is deleted (/dv)

**Find this in `qbx_core/server/commands.lua`:**

```lua
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

    if pedCars[1] == 0 or radius then
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

**Replace with:**

```lua
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

    if pedCars[1] == 0 or radius then
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

{% hint style="info" %}
If you use a third-party admin menu that registers its own `/car` or `/dv` command, add the key removal export there as well using the same pattern as Step 3.
{% endhint %}

