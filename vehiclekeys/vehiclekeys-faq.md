---
icon: newspaper
description: Heres a list of common questions and answers around the script :)
---

# FAQ

FAQ

<details>

<summary>Why is the car still on when I get out?</summary>

Vehicles will remain on when getting out of them, this is an intended feature that adds to immersion but is available to change in the config.&#x20;

</details>

<details>

<summary>How do I make my script work with keys?</summary>

If you are running into issues on compatibility please make a ticket in the discord and we will try to help. The exports are also available on this documentation page.

</details>

<details>

<summary>Do lockpicks work? </summary>

Yes, these are registered as usable items located in the init file for "lockpick" and "advancedlockpick".

If you use a house robbery that registers it then that one will take priority but the codes open.

</details>

<details>

<summary>My Police/EMS Jobs are getting a ton of keys, is there any way to make them have less?</summary>

<pre><code><strong>In the config there is a spot called JobBypassKeys, inside there add the
</strong><strong>job name and vechicle spawn model. ie police dont need to be given keys to police
</strong></code></pre>

</details>

<details>

<summary>My Friends Cant Drive My Car Without Hotwiring it!</summary>

<pre><code><strong>When using item based keys you can give them the key, or if you go to the locksmith
</strong><strong>you can buy a spare key for them. If not using item based you may give keys with
</strong><strong>/givekeys or through the /keyring command
</strong></code></pre>

</details>

<details>

<summary>I own a car but its not in my garage table, how can I get a spare?</summary>

<pre><code><strong>Because of the way the frameworks store owned vehicles ie player_vehicles etc
</strong><strong>these are the only tables the locksmith supports. Scripts like trucking scripts
</strong><strong>will need to grant keys on spawn.
</strong><strong>We are a config in many scripts by defualt (including lc_truck_logisitics inside their lc_utils)
</strong></code></pre>

</details>

<details>

<summary>Is there a way we can use keys without needing the item?</summary>



Yes! The config supports this

```lua
Config.ItemBasedSettings = {
	using_key_items = true -- set to false to not use keys as items :)
```

</details>

<details>

<summary>Do you have backwards compatibility with qb-vehiclekeys events?</summary>

Yes, All standard qb-vehiclekey events are available to use. It is highly recommended to use the direct exports for the scrips enhanced features though.&#x20;

</details>



