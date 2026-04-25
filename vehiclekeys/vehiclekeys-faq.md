---
description: Heres a list of common questions and answers around the script :)
icon: newspaper
---

# FAQ

FAQ

<details>

<summary><em><strong>Why is the car still on when I get out?</strong></em></summary>

#### **This is a preference available in the config, search for**

```lua
EngineRemainsOnWhenExiting = false,									-- set this to true to keep a vehicle running when exiting it, this is a more realistic approach where youd have to turn it off when getting out or leave it on if you want to plan an escape etc.
```

</details>

<details>

<summary>How do I make my script work with keys?</summary>

You will need to add the exports for the key grants, please see the export documentation.

[https://mrnewbs-scrips.gitbook.io/guide/vehiclekeys/vehicle-keys-exports](https://mrnewbs-scrips.gitbook.io/guide/vehiclekeys/vehicle-keys-exports)

</details>

<details>

<summary>Do lockpicks work?</summary>

Yes, these are registered as usable items located in the init file for "lockpick" and "advancedlockpick".

If you use a house robbery that registers it then that one will take priority but the codes open for them if any adjustment is needed.

</details>

<details>

<summary>My Police/EMS Jobs are getting a ton of keys, is there any way to make them have less?</summary>

In the config, there is a section called JobBypassKeys. Add the job name and vehicle spawn model there. For example, police officers don't need to be given keys to police vehicles.

</details>

<details>

<summary>My Friends Cant Drive My Car Without Hotwiring it!</summary>

When using item-based keys, you can either give them the key directly or purchase a spare key from the locksmith. If not using item-based keys, you can grant access using the /givekeys command or manage keys through the /keyring command.

</details>

<details>

<summary>I own a car but its not in my garage table, how can I get a spare?</summary>

Due to how frameworks store owned vehicles (e.g., player\_vehicles), these are the only tables the locksmith supports. Scripts like trucking scripts will need to grant keys upon vehicle spawn. We are included as a default config in many scripts, including _lc\_truck\_logistics_ within their _lc\_utils_.

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

Yes, All standard qb-vehiclekey events are available to use. It is highly recommended to use the direct exports for the scrips enhanced features though.

</details>
