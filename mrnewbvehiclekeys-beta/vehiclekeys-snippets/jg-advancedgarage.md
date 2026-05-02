---
icon: j
---

# jg-advancedgarage

{% hint style="info" %}
`jg-advancedgarage` has native support for multiple key systems. No code changes are required — simply point the key system config option to `MrNewbVehicleKeys` and the script will call the correct exports automatically.
{% endhint %}

{% hint style="success" %}
This is the preferred type of integration: use the script's built-in key-system setting instead of patching source files manually.
{% endhint %}

## Configuration

Open `jg-advancedgarage/config/config.lua` and set the key system to `MrNewbVehicleKeys`:

<figure><img src="../../.gitbook/assets/image.png" alt="The jg-advancedgarage key system config option set to MrNewbVehicleKeys"><figcaption><p>Set the <strong>Keys</strong> config option to <strong>MrNewbVehicleKeys</strong></p></figcaption></figure>

{% hint style="success" %}
That's all that's needed. Keys will be given when a vehicle is retrieved from the garage and removed when it is stored.
{% endhint %}

{% hint style="info" %}
After changing the config, test one vehicle retrieval and one vehicle store action to confirm the selected key system is being used.
{% endhint %}

Get it here if you don't have it: [https://jgscripts.com/scripts/advanced-garages](https://jgscripts.com/scripts/advanced-garages)
