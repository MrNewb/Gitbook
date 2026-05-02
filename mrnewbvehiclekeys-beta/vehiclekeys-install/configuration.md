---
description: Full configuration reference for MrNewbVehicleKeys.
icon: remote
---

# Configuration

This is the default `configs/config.lua`. Adjust the values to match your server's needs.

{% hint style="info" %}
If this is your first setup, complete the [install steps](./), framework setup, and inventory items before touching the config.
{% endhint %}

```lua
Config = Config or {}

Config.DebugMode = false -- Please do not enable this unless in a ticket, it does not do what you think. This does not give debug prints for everything, only a few select things that I need to test. Enabling this will cause a LOT of debug prints that are not useful to anyone but me.
Config.EnableUI = true

Config.Hotwire = {
    Enabled = true,
    SyncedHotwires = true,       -- Sync hotwire status across all clients via statebags
    MaxHotwireAttempts = 3,      -- Maximum number of hotwire attempts before vehicle becomes immune
    HotwireTime = 5000,          -- Time in milliseconds that the hotwire will take
    HotwireFailChance = 50,      -- Percentage chance that a hotwire will fail
    GiveKey = true,              -- Give player a key after hotwiring
    TimeBetweenHotwires = 10000, -- Time in milliseconds before player can attempt hotwire again
    Animation = {
        animDict = "veh@handler@base",
        anim = "hotwire",
    },
    Minigame = {
        Type = "ox_lib",        -- Options: "ox_lib", "bagus", "ps-ui", "bl-progress", "bl-keyspam", "bl-circle", "bl-printlock", "t3_lockpick", "xmmx", "rainmadlockpick", "rainmadaction", "rainmadquick", "rainmadmash", "rainmadangled", "false"
        Difficulty = "easy",    -- Options: "easy", "medium", "hard"
        Rounds = 3,
    },
    RequireItem = {
        Enabled = false,        -- Incomplete, not ready for use
        Item = "hotwire_kit",
        UseTime = 10000,
    },
}

Config.VehicleSettings = {
    LockSounds = true,                      -- Enable lock/unlock sounds
    DisableVehicleAutoStart = true,         -- Prevents vehicles from auto-starting when entering
    HotwireDisabled = false,                -- Disable hotwire features entirely
    EngineRemainsOnWhenExiting = true,      -- Keep engine running when exiting vehicle
    GiveKeysIfEngineRunning = true,         -- Auto-give keys if engine is running when entering as driver
    SuspensionBounceEnabled = true,         -- Play suspension animation on lock/unlock
    FrontTrunkVehicle = {
        [`adder`] = 4,
        [`reaper`] = 4,
        [`torero`] = 5,
        [`t20`] = 4,
    },
}

Config.ItemBasedSettings = {
    Enabled = true,                            -- true = keys are inventory items, false = keys are stored in database/memory
    CheckOverride = 5000,
    EnableAftermarketLocks = true,
    IncludePlayerNameInKeyDescription = true,
}

Config.SearchForKeys = {
    Enabled = true,
    SearchTime = 5000,
    MaxSearchAttempts = 3,
    Chance = 50,               -- Percentage chance to find keys (1-100)
    SearchableItems = {
        {name = "lockpick", count = 1},
        {name = "radio", count = 1, metadata = {description = "A radio device."}},
    },
}

Config.Keybinds = {
    OpenKeyRing = "F2",
    OpenKeyFob = "F3",
    LockVehicle = "L",
    Hotwire = "E",
    SearchVehicle = "H",
    EngineToggle = "F10",
    AdjustAutoPilot = "E",
}

Config.Blacklist = {
    ["No Key Required Vehicles"] = {
        [`bmx`] = true,
        [`cruiser`] = true,
        [`scorcher`] = true,
        [`tribike2`] = true,
        [`tribike3`] = true,
        [`fixter`] = true,
        [`tribike`] = true,
        [`inductor`] = true,
        [`inductor2`] = true,
    },
    ["No Key Required Plates"] = {
        ["Farts"] = true,
        ["Delivery"] = true,
    },
    ["Hotwire Immune Vehicles"] = {
        [`police`] = true,
        [`ambulance`] = true,
        [`firetruk`] = true,
    },
    ["Hotwire Immune Plates"] = {
        ["Farts"] = true,
        ["Delivery"] = true,
    },
    ["Lockpick Immune Vehicles"] = {
        [`police`] = true,
        [`ambulance`] = true,
        [`firetruk`] = true,
    },
    ["Advanced Lockpick Required Vehicles"] = {
        [`taxi`] = true,
        [`towtruck`] = true,
        [`towtruck2`] = true,
        [`flatbed`] = true,
    },
    ["Shared Job Models"] = {
        police = {
            [`police`] = true,
            [`police2`] = true,
            [`police3`] = true,
            [`police4`] = true,
            [`policeb`] = true,
            [`policet`] = true,
            [`polmav`] = true,
        },
        ambulance = {
            [`ambulance`] = true,
        },
    },
    ["Shared Job Plates"] = {
        police = {
            "BIGBOSS",
            "CALLSIGN",
        },
    }
}

Config.Lockpicks = {
    Enabled = true,
    BreakChance = 50,
    BreakOnSuccess = false,
    LockpickAlarmTime = 3000,
    LockpickItem = "lockpick",
    AdvancedLockpickItem = "advancedlockpick",
    Minigame = {
        Type = "ox_lib",                -- "ox_lib", "bagus", "ps-ui", "bl-progress", "bl-keyspam", "bl-circle", "bl-printlock", "t3_lockpick", "xmmx", "rainmadlockpick", "rainmadaction", "rainmadquick", "rainmadmash", "rainmadangled", "false"
        Difficulty = "medium",
        AdvancedDifficulty = "hard",
    },
}

Config.LockNpcCars = {
    Enabled = true,
    LockChance = 10,
    ImmuneModels = {
        [`bmx`] = true,
    },
}

Config.CustomCarsMissingLabels = {
    {model = "aerocab", label = "Aerocab"},
    {model = "blacktop", label = "Blacktop"},
    {model = "brickades", label = "Brickades"},
    {model = "linerunner", label = "linerunner"},
    {model = "vetirs", label = "Vetirs"},
}

Config.ProximityLocking = {
    Enabled = true,
    PlayerDefaults = true,
    LockDistance = 10.0,
    UnlockDistance = 5.0,
    StoreGracePeriod = 2500,
}

Config.Dispatch = {
    Enabled = true,
    AlertChances = {
        HotwireAlertChance = 50,
        LockpickAlertChance = 50,
        HijackingAlertChance = 50,
    },
    ReceiveAlerts = {
        "police",
        "ambulance",
        "sheriff"
    },
}

Config.LockSmith = {
    Enabled = true,
    EnableKeyRing = false,
    EnableFobUpgrades = true,
    FobUpgradesOnOwnedOnly = false,
    Pricing = {
        SpareKey = {
            cost = 100,
            currencies = {"cash", "bank"},
        },
        Items = {
            lockpick = {
                label = "Lockpick",
                count = 1,
                cost = 500,
                currencies = {"cash", "bank"},
            },
            advancedlockpick = {
                label = "Advanced Lockpick",
                count = 1,
                cost = 10000,
                currencies = {"cash", "bank"},
            },
            keyring = {
                label = "Keyring",
                count = 1,
                cost = 500,
                currencies = {"cash", "bank"},
            },
            aftermarket_locks = {
                label = "Aftermarket Lock System",
                count = 1,
                cost = 15000,
                currencies = {"cash", "bank"},
            },
        },
    },
    Locations = {
        ["Locksmith"] = {
            coords = vector4(170.3532, -1799.5085, 28.34, 327.1338),
            entityType = "ped",
            model = "a_m_y_vindouche_01",
            distance = 100,
            Blip = {
                enabled = true,
                sprite = 811,
                color = 1,
                display = 4,
                scale = 0.8,
            },
        },
    },
    GlobalTargets = {
        -- Add ped models here to make them locksmith entities everywhere they spawn
    },
}

Config.GlobalVehicleTargets = {
    Enabled = true,
    LockVehicle = {
        Enabled = true,
        Distance = 3.0,
    },
    UnLockVehicle = {
        Enabled = true,
        Distance = 3.0,
    },
    StartEngine = {
        Enabled = true,
        Distance = 3.0,
    },
    TurnOffEngine = {
        Enabled = true,
        Distance = 3.0,
    },
    ToggleRoof = {
        Enabled = true,
        Distance = 3.0,
    },
    ForceUnlock = {
        Enabled = true,
        Distance = 1.5,
    },
}

Config.VehicleForceUnlock = {
    Enabled = true,
    MaxDistance = 2.5,
    ProgressBar = {
        Duration = 5000,
        CanCancel = true,
        Animation = {
            dict = "melee@knife@streamed_variations",
            clip = "vehicle_kick_var_a",
        },
    },
    EnabledJobs = {
        "ambulance",
        "mechanic",
        "police",
    },
}

Config.ParkingSpots = {} -- Populated at runtime, leave empty

Config.KeyJobStorages = {
    Enabled = true,
    Locations = {
        ["police_key_holder"] = {
            jobName = "police",
            model = "s_m_y_cop_01",
            entityType = "ped",
            coords = vector4(441.2985, -1013.6700, 27.6370, 174.8269),
            stashId = "police_key_stash",
            label = "Police Key Holder",
            -- blip = {
            --     enabled = true,
            --     sprite = 498,
            --     color = 0,
            --     scale = 0.8,
            -- },
        },
        ["police_key_box"] = {
            jobName = {"police", "mechanic"}, -- single job string or array of jobs
            model = "prop_parkingpay",
            entityType = "object",
            coords = vector4(419.1602, -986.2368, 28.3910, 270.1254),
            stashId = "police_key_stash_box",
            label = "Police Deposit Box",
            -- blip = {
            --     enabled = true,
            --     sprite = 498,
            --     color = 0,
            --     scale = 0.8,
            -- },
        },
        -- ["mechanic_key_holder"] = {
        --     jobName = "mechanic",
        --     model = "a_m_m_business_2",
        --     entityType = "ped",
        --     coords = vector4(0, 0, 0, 0.0),
        --     stashId = "mechanic_key_stash",
        --     label = "Mechanic Key Holder",
        -- },
    },
}
```
