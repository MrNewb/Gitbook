---
icon: faucet
---

# Common qb-core Snippets

## DV Command — Remove Keys on Vehicle Delete

When a vehicle is deleted via the `/dv` command, keys should be removed first so they do not linger in the player's inventory or key list.

{% hint style="warning" %}
Find the event handler in your qb-core install and replace it with the version below. Do **not** apply both versions at the same time.
{% endhint %}

**Find this:**

```lua
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

**Replace with:**

```lua
RegisterNetEvent('QBCore:Command:DeleteVehicle', function()
    local ped = PlayerPedId()
    local veh = GetVehiclePedIsUsing(ped)
    if veh ~= 0 then
        SetEntityAsMissionEntity(veh, true, true)
        exports.MrNewbVehicleKeys:RemoveKeys(veh)
        Wait(100)
        DeleteVehicle(veh)
    else
        local pcoords = GetEntityCoords(ped)
        local vehicles = GetGamePool('CVehicle')
        for _, v in pairs(vehicles) do
            if #(pcoords - GetEntityCoords(v)) <= 5.0 then
                SetEntityAsMissionEntity(v, true, true)
                exports.MrNewbVehicleKeys:RemoveKeys(v)
                Wait(100)
                DeleteVehicle(v)
            end
        end
    end
end)
```

***
