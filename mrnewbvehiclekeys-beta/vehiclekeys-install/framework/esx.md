---
description: >-
  To install MrNewbVehicleKeys to the frameworks /car command you will need to
  do these edits, This will need to be adjusted in any third party admin menus
  in a similar method.
icon: tombstone
---

# esx

{% hint style="warning" %}
If you were previously using another key script, make sure it is removed or disabled before starting MrNewbVehicleKeys.
{% endhint %}

## Step 1 — Edit the /car command

This gives the admin keys to any vehicle they spawn via `/car`.

**Find this in `es_extended/server/commands.lua` (around line 69):**

```lua
-- Find This in es_extended/server/commands.lua aprox around line 69

ESX.RegisterCommand(
    "car",
    "admin",
    function(xPlayer, args, showError)
        if not xPlayer then
            return showError("[^1ERROR^7] The xPlayer value is nil")
        end

        local playerPed = GetPlayerPed(xPlayer.source)
        local playerCoords = GetEntityCoords(playerPed)
        local playerHeading = GetEntityHeading(playerPed)
        local playerVehicle = GetVehiclePedIsIn(playerPed)

        if not args.car or type(args.car) ~= "string" then
            args.car = "adder"
        end

        if playerVehicle then
            DeleteEntity(playerVehicle)
        end

        if Config.AdminLogging then
            ESX.DiscordLogFields("UserActions", "Spawn Car /car Triggered!", "pink", {
                { name = "Player", value = xPlayer and xPlayer.name or "Server Console", inline = true },
                { name = "ID", value = xPlayer and xPlayer.source or "Unknown ID", inline = true },
                { name = "Vehicle", value = args.car, inline = true },
            })
        end

        ESX.OneSync.SpawnVehicle(args.car, playerCoords, playerHeading, upgrades, function(networkId)
            if networkId then
                local vehicle = NetworkGetEntityFromNetworkId(networkId)
                for _ = 1, 20 do
                    Wait(0)
                    SetPedIntoVehicle(playerPed, vehicle, -1)

                    if GetVehiclePedIsIn(playerPed, false) == vehicle then
                        break
                    end
                end
                if GetVehiclePedIsIn(playerPed, false) ~= vehicle then
                    showError("[^1ERROR^7] The player could not be seated in the vehicle")
                end
            end
        end)
    end,
    false,
    {
        help = TranslateCap("command_car"),
        validate = false,
        arguments = {
            { name = "car", validate = false, help = TranslateCap("command_car_car"), type = "string" },
        },
    }
)
```

**Replace with:**

```lua
ESX.RegisterCommand(
    "car",
    "admin",
    function(xPlayer, args, showError)
        if not xPlayer then
            return showError("[^1ERROR^7] The xPlayer value is nil")
        end

        local playerPed = GetPlayerPed(xPlayer.source)
        local playerCoords = GetEntityCoords(playerPed)
        local playerHeading = GetEntityHeading(playerPed)
        local playerVehicle = GetVehiclePedIsIn(playerPed)

        if not args.car or type(args.car) ~= "string" then
            args.car = "adder"
        end

        if playerVehicle then
            DeleteEntity(playerVehicle)
        end

        if Config.AdminLogging then
            ESX.DiscordLogFields("UserActions", "Spawn Car /car Triggered!", "pink", {
                { name = "Player", value = xPlayer and xPlayer.name or "Server Console", inline = true },
                { name = "ID", value = xPlayer and xPlayer.source or "Unknown ID", inline = true },
                { name = "Vehicle", value = args.car, inline = true },
            })
        end

        ESX.OneSync.SpawnVehicle(args.car, playerCoords, playerHeading, upgrades, function(networkId)
            if networkId then
                local vehicle = NetworkGetEntityFromNetworkId(networkId)
                for _ = 1, 20 do
                    Wait(0)
                    SetPedIntoVehicle(playerPed, vehicle, -1)
                    if GetVehiclePedIsIn(playerPed, false) == vehicle then
                        exports.MrNewbVehicleKeys:GiveKeys(xPlayer.source, networkId)
                        break
                    end
                end
                if GetVehiclePedIsIn(playerPed, false) ~= vehicle then
                    showError("[^1ERROR^7] The player could not be seated in the vehicle")
                end
            end
        end)
    end,
    false,
    {
        help = TranslateCap("command_car"),
        validate = false,
        arguments = {
            { name = "car", validate = false, help = TranslateCap("command_car_car"), type = "string" },
        },
    }
)
```

---

{% hint style="info" %}
If you use a third-party admin menu that registers its own `/car` command, you will need to add `exports.MrNewbVehicleKeys:GiveKeys` there too, using the same pattern as above.
{% endhint %}
