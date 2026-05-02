---
description: Snippet example use case in wasabi_bridge.
icon: car
---

# wasabi\_bridge

This shows how to add MrNewbVehicleKeys support to `wasabi_bridge`. You will also need to adjust the relevant config options in Wasabi's scripts to route key actions through the bridge.

{% hint style="info" %}
Edit `wasabi_bridge/customize/client/carkeys.lua`. Both the give and remove functions need updating.
{% endhint %}

{% hint style="warning" %}
This is a bridge integration. Make sure the surrounding Wasabi config is also set to use the bridge path you are editing, otherwise these changes may never be called.
{% endhint %}

**Find this:**

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

**Replace with:**

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

{% hint style="success" %}
Once updated, test both directions: a flow that grants keys through the bridge and a flow that removes keys, so you know the bridge is routing both actions correctly.
{% endhint %}
