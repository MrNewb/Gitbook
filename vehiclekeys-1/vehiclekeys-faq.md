---
description: Common questions and answers about MrNewbVehicleKeys.
icon: newspaper
---

# FAQ

{% hint style="info" %}
Can't find an answer here? Join the support Discord or open a ticket on Tebex.
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

You will need to add the exports for the key grants, please see the export documentation.

[https://mrnewbs-scrips.gitbook.io/guide/vehiclekeys/vehicle-keys-exports](https://mrnewbs-scrips.gitbook.io/guide/vehiclekeys/vehicle-keys-exports)

</details>

<details>

<summary>Do lockpicks work?</summary>

Yes. Lockpicks and advanced lockpicks are registered as usable items in the resource's `init` file. If another script (e.g. a house robbery script) registers its own lockpick item, that one will take priority — but the code is open if you need to adjust it.

</details>

<details>

<summary>My Police/EMS jobs are getting too many keys — is there a way to reduce that?</summary>

Yes. In the config there is a `JobBypassKeys` section. Add the job name and vehicle spawn model there and those players will not be given keys for matching vehicles automatically — for example, police officers do not need keys granted for police vehicles.

</details>

<details>

<summary>My friends can't drive my car without hotwiring it!</summary>

When using item-based keys, you can either give them the key directly from your keyring, or purchase a spare key from the locksmith. If you are not using item-based keys, you can grant access with the `/givekeys` command or through the `/keyring` menu.

</details>

<details>

<summary>I own a car but it's not in the garage table — how can I get a spare key?</summary>

The locksmith only supports vehicles stored in framework-standard tables (e.g. `player_vehicles`). Scripts that spawn vehicles outside of that (such as trucking scripts) will need to grant keys on vehicle spawn. MrNewbVehicleKeys is included as a default config in several scripts, including _lc\_truck\_logistics_ via _lc\_utils_.

</details>

<details>

<summary>Is there a way we can use keys without needing the item?</summary>

Yes! The config supports this option

```lua
Config.ItemBasedSettings = {
	using_key_items = true -- set to false to not use keys as items :)
```

</details>

<details>

<summary>Do you have backwards compatibility with qb-vehiclekeys events?</summary>

Yes, All standard qb-vehiclekey events are available to use. It is highly recommended to use the direct exports for the scrips enhanced features though.&#x20;

</details>



