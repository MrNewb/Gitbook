---
description: Snippet example use case in qbx_adminmenu.
icon: car
---

# qbx\_adminmenu

{% hint style="info" %}
The clientside of this uses a generic qb-vehiclekeys event that we can already use, the server side has a hardcoded export instead of using the framework options so we must adjust this.
{% endhint %}

## Find this

Locate this inside qbx\_adminmenu/server/main.lua around line 303 ([https://github.com/Qbox-project/qbx\_adminmenu/blob/90c674ebdbb262d43e8d9534e3c7c056d56f91e8/server/main.lua#L303-L316](https://github.com/Qbox-project/qbx_adminmenu/blob/90c674ebdbb262d43e8d9534e3c7c056d56f91e8/server/main.lua#L303-L316))

```lua
lib.callback.register('qbx_admin:server:spawnVehicle', function(source, model)
    if not IsPlayerAceAllowed(source, config.commandPerms.spawnVehicle) then exports.qbx_core:Notify(source, locale('error.no_perms'), 'error') return end
    if not exports.qbx_core:IsOptin(source) then exports.qbx_core:Notify(source, locale('error.not_optin'), 'error') return end

    local ped = GetPlayerPed(source)
    local netId, vehicle = qbx.spawnVehicle({
        model = model,
        spawnSource = ped,
        warp = true,
    })

    exports.qbx_vehiclekeys:GiveKeys(source, vehicle)
    return netId
end)
```

## Replace with this

```lua
lib.callback.register('qbx_admin:server:spawnVehicle', function(source, model)
    if not IsPlayerAceAllowed(source, config.commandPerms.spawnVehicle) then exports.qbx_core:Notify(source, locale('error.no_perms'), 'error') return end
    if not exports.qbx_core:IsOptin(source) then exports.qbx_core:Notify(source, locale('error.not_optin'), 'error') return end

    local ped = GetPlayerPed(source)
    local netId, vehicle = qbx.spawnVehicle({
        model = model,
        spawnSource = ped,
        warp = true,
    })

    --exports.qbx_vehiclekeys:GiveKeys(source, vehicle)
    exports.MrNewbVehicleKeys:GiveKeys(source, netId)
    return netId
end)
```
