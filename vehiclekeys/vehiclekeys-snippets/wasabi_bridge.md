---
description: Snippet example use case in wasabi_bridge.
icon: car
---

# wasabi\_bridge

Here is how to add MrNewbVehicleKeys compatibility to wasabi\_bridge, keep in mind you will have to adjust config options in his scripts to make this work with it.

## find this in wasabi\_bridge/customize/client/carkeys.lua

```lua
-- Add car keys
function WSB.giveCarKeys(plate, _model, _vehicle)
    print(GetResourceState('wasabi_carlock'))
    if GetResourceState('wasabi_carlock') == 'started' then
        return exports.wasabi_carlock:GiveKey(plate) -- Leave like this if using wasabi_carlock
    end

    if GetResourceState('qb-vehiclekeys') == 'started' then
        return TriggerServerEvent('qb-vehiclekeys:server:AcquireVehicleKeys', plate)
    end
end

function WSB.removeCarKeys(plate, _model, _vehicle)
    if GetResourceState('wasabi_carlock') == 'started' then
        return exports.wasabi_carlock:RemoveKey(plate)
    end
end
```

## Change it to this

```lua
-- Add car keys
function WSB.giveCarKeys(plate, _model, _vehicle)
    if GetResourceState('wasabi_carlock') == 'started' then
        return exports.wasabi_carlock:GiveKey(plate) -- Leave like this if using wasabi_carlock
    end
    if GetResourceState('MrNewbVehicleKeys') == 'started' then
        return exports.MrNewbVehicleKeys:GiveKeysByPlate(plate)
    end
    if GetResourceState('qb-vehiclekeys') == 'started' then
        return TriggerServerEvent('qb-vehiclekeys:server:AcquireVehicleKeys', plate)
    end
end

function WSB.removeCarKeys(plate, _model, _vehicle)
    if GetResourceState('wasabi_carlock') == 'started' then
        return exports.wasabi_carlock:RemoveKey(plate)
    end
    if GetResourceState('MrNewbVehicleKeys') == 'started' then
        return exports.MrNewbVehicleKeys:RemoveKeysByPlate(plate)
    end
end
```
