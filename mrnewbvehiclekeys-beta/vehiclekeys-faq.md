---
description: Common questions and answers about MrNewbVehicleKeys.
icon: newspaper
---

# FAQ

{% hint style="info" %}
Can't find an answer here? Join the support Discord or open a ticket on Tebex.
{% endhint %}

{% hint style="success" %}
If you are troubleshooting a fresh install, check the install guide first, then the configuration guide, then come back here for edge cases and workflow questions.
{% endhint %}

## Quick Links

| Need something specific? | Page |
| --- | --- |
| Commands and keybinds | [Commands](vehiclekeys-faq-1.md) |
| Server and client exports | [Exports](vehicle-keys-exports/README.md) |
| Install steps | [Install Guide](vehiclekeys-install/README.md) |
| Config reference | [Configuration Guide](vehiclekeys-install/configuration.md) |

## Before Asking For Support

If you end up in Discord or on Tebex support, having these details ready will usually save a round of back-and-forth:

| Bring this | Why it helps |
| --- | --- |
| Script version | Confirms the exact build being used |
| Framework and inventory | Rules out integration-specific behavior |
| Item-based on or off | Changes how keys are stored and removed |
| The exact workflow that failed | Helps reproduce the issue quickly |
| Any console or F8 error text | Surfaces the real failure point |

{% hint style="info" %}
The more specific the report, the faster support can point you to the right config, export, or integration fix.
{% endhint %}

<details>

<summary>Why is the car still on when I get out?</summary>

This is a config preference. Search for `EngineRemainsOnWhenExiting` in `config.lua` and set it to `true` to keep the engine running when you exit a vehicle.

```lua
EngineRemainsOnWhenExiting = false, -- set to true to keep the vehicle running on exit
```

</details>

<details>

<summary>How do I make my script work with keys?</summary>

You will usually want to add the direct MrNewbVehicleKeys exports wherever another resource spawns, stores, sells, rents, or removes access to a vehicle.

{% hint style="info" %}
Start with the [Exports](vehicle-keys-exports/README.md) page for API usage, or the [Snippet Examples](vehiclekeys-snippets/README.md) page if you want copy-paste integration patterns for common resources.
{% endhint %}

</details>

<details>

<summary>Do lockpicks work?</summary>

Yes. Lockpicks and advanced lockpicks are registered as usable items in the resource's `init` file. If another script (e.g. a house robbery script) registers its own lockpick item, that one will take priority — but the code is open if you need to adjust it.

{% hint style="info" %}
Lockpick difficulty, break chance, and advanced lockpick behavior are all configured under `Config.Lockpicks`.
{% endhint %}

</details>

<details>

<summary>My Police/EMS jobs are getting too many keys — is there a way to reduce that?</summary>

Yes. In `configs/config.lua` there is a `Config.Blacklist` table with `"Shared Job Models"` and `"Shared Job Plates"` sections. Add the job name and vehicle models/plates there — players in that job will not be auto-granted keys for those vehicles:

{% hint style="info" %}
This is the main balancing tool for shared fleets, emergency services, and other job vehicles that should not hand out permanent keys too freely.
{% endhint %}

```lua
Config.Blacklist = {
    ["Shared Job Models"] = {
        police = {
            [`police`] = true,
            [`police2`] = true,
        },
        ambulance = {
            [`ambulance`] = true,
        },
    },
    ["Shared Job Plates"] = {
        police = {
            "BIGBOSS",
        },
    }
}
```

</details>

<details>

<summary>My friends can't drive my car without hotwiring it!</summary>

When using item-based keys, you can either give them the key directly from your keyring, or purchase a spare key from the locksmith. If you are not using item-based keys, you can grant access with the `/givekeys` command or through the `/keyring` menu.

{% hint style="info" %}
If another resource is granting keys, prefer the direct server exports so you can use optional behavior such as `autoKeyring`.
{% endhint %}

If you are granting item-based keys from another resource, the server exports also support an optional `autoKeyring` argument. Setting that to `true` will store the granted key directly inside the player's `keyring` item when they have one, instead of creating a separate `vehiclekeys` item.

</details>

<details>

<summary>I own a car but it's not in the garage table — how can I get a spare key?</summary>

The locksmith only supports vehicles stored in framework-standard tables (e.g. `player_vehicles`). Scripts that spawn vehicles outside of that (such as trucking scripts) will need to grant keys on vehicle spawn. MrNewbVehicleKeys is included as a default config in several scripts, including _lc\_truck\_logistics_ via _lc\_utils_.

{% hint style="info" %}
If a third-party script creates vehicles outside your normal owned-vehicle flow, that script should grant keys directly when it spawns the vehicle.
{% endhint %}

</details>

<details>

<summary>Is there a way we can use keys without needing the item?</summary>

Yes. In `configs/config.lua`, set `Enabled` to `false` inside `Config.ItemBasedSettings`:

```lua
Config.ItemBasedSettings = {
    Enabled = false, -- set to false to disable item-based keys
    ...
}
```

When disabled, keys are stored in the database/memory rather than as inventory items.

</details>

<details>

<summary>Do you have backwards compatibility with qb-vehiclekeys events?</summary>

Yes. Standard qb-vehiclekeys compatibility events are available for migration, but direct exports are still the preferred option for new integrations and enhanced features.

{% hint style="info" %}
Backwards compatibility is helpful for migration, but new integrations should use the native MrNewbVehicleKeys exports whenever possible.
{% endhint %}

</details>



