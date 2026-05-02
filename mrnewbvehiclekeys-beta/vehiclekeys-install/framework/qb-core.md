---
description: To install MrNewbVehicleKeys to the core you will need use this snippet
icon: faucet-drip
---

# qb-core

{% hint style="warning" %}
Remove or disable `qb-vehiclekeys` before starting MrNewbVehicleKeys. Backwards-compatible qb-vehiclekeys events are supported, so existing scripts will continue to work.
{% endhint %}

## Step 1 — Remove keys when a vehicle is deleted (/dv)

**Find this in `qb-core/client/events.lua` (around line 144):**

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

---

## Step 2 — Add items to qb-core/shared/items.lua

Both the old and new QB item formats are provided below — use whichever matches your version.

**Old format:**

```lua
['vehiclekeys'] 	    = {['name'] = 'vehiclekeys',        ['label'] = 'Vehicle Keys',            ['weight'] = 100,  ['type'] = 'item', ['image'] = 'vehiclekeys.png',         ['unique'] = true,  ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'Fancy vehicle keys'},
['keyring'] 		    = {['name'] = 'keyring',            ['label'] = 'Keyring',                 ['weight'] = 220,  ['type'] = 'item', ['image'] = 'keyring.png',             ['unique'] = true,  ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'A keyring that holds car keys.'},
['aftermarket_locks']   = {['name'] = 'aftermarket_locks',  ['label'] = 'Aftermarket Lock System', ['weight'] = 220,  ['type'] = 'item', ['image'] = 'aftermarket_locks.png',   ['unique'] = false, ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'A Vehicle Lock System To Replace Key Systems'},
['lockpick'] 		    = {['name'] = 'lockpick',           ['label'] = 'Lockpick',                ['weight'] = 850,  ['type'] = 'item', ['image'] = 'lockpick.png',            ['unique'] = false, ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'A mysterious device.'},
['advancedlockpick']    = {['name'] = 'advancedlockpick',   ['label'] = 'Advanced Lockpick',       ['weight'] = 850,  ['type'] = 'item', ['image'] = 'advancedlockpick.png',    ['unique'] = false, ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'A upgraded mysterious device.'},
['rental_paperwork']    = {['name'] = 'rental_paperwork',   ['label'] = 'Rental Paperwork',        ['weight'] = 850,  ['type'] = 'item', ['image'] = 'rental_paperwork.png',    ['unique'] = true,  ['useable'] = true, ['shouldClose'] = true, ['combinable'] = nil, ['description'] = 'Paperwork for a rental vehicle.'},
```

**New format:**

```lua
vehiclekeys       = { name = 'vehiclekeys',       label = 'Vehicle Keys',            weight = 100, type = 'item', image = 'vehiclekeys.png',         unique = true,  useable = true, shouldClose = true, combinable = nil, description = 'Fancy vehicle keys' },
keyring           = { name = 'keyring',           label = 'Vehicle Key Ring',        weight = 100, type = 'item', image = 'keyring.png',             unique = true,  useable = true, shouldClose = true, combinable = nil, description = 'A keyring to solve all problems.' },
aftermarket_locks = { name = 'aftermarket_locks', label = 'Aftermarket Lock System', weight = 100, type = 'item', image = 'aftermarket_locks.png',   unique = true,  useable = true, shouldClose = true, combinable = nil, description = 'A Vehicle Lock System To Replace Key Systems' },
lockpick          = { name = 'lockpick',          label = 'Lockpick',                weight = 300, type = 'item', image = 'lockpick.png',            unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A mysterious device.' },
advancedlockpick  = { name = 'advancedlockpick',  label = 'Advanced Lockpick',       weight = 500, type = 'item', image = 'advancedlockpick.png',    unique = false, useable = true, shouldClose = true, combinable = nil, description = 'A upgraded mysterious device.' },
rental_paperwork  = { name = 'rental_paperwork',  label = 'Rental Paperwork',        weight = 850, type = 'item', image = 'rental_paperwork.png',    unique = true,  useable = true, shouldClose = true, combinable = nil, description = 'Paperwork for a rental vehicle.' },
```

{% hint style="info" %}
If you use a third-party admin menu that registers its own `/car` or `/dv` command, add the `RemoveKeys` export there as well using the same pattern as Step 1.
{% endhint %}

