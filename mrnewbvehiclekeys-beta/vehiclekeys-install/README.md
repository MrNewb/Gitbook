---
description: Install Guide
icon: wrench
---

# Install

This guide gets the base resource running in the right order before you move on to framework hooks, inventory items, and gameplay tuning.

## Install Flow

1. Set the correct resource start order.
2. Follow the framework guide for your core.
3. Add the required inventory items and images.
4. Review the configuration guide, then test the full vehicle flow before going live.

## Configuration

After the base install is working, use the [Configuration Guide](configuration.md) to tune gameplay, pricing, keyring behavior, dispatch, and shared key storage. It also covers the optional `provide` aliases in `fxmanifest.lua` for migration setups.

## Start Order

MrNewbVehicleKeys must start **after** your inventory, target, ox\_lib, and community\_bridge resources. Many scripts (including this one) use auto-detection to check if a resource is running, so start order matters.

{% hint style="warning" %}
This is an example only — do not copy it directly into your config. Adjust the resource names to match what you actually have installed.
{% endhint %}

```
ensure ox_lib
ensure <your_framework>         # e.g. qb-core, es_extended, qbx_core
ensure <your_inventory>         # e.g. ox_inventory, qb-inventory
ensure <your_target>            # e.g. ox_target, qb-target
ensure community_bridge
ensure MrNewbVehicleKeys
ensure <your_garage>            # e.g. qb-garages, ox_garage
```

{% hint style="info" %}
**community\_bridge** is required. You can find it here: [https://github.com/MrNewb/community\_bridge](https://github.com/MrNewb/community_bridge)
{% endhint %}

{% hint style="success" %}
Once the script starts cleanly, test one complete workflow end to end: retrieve or spawn a vehicle, confirm access, lock and unlock it, and then verify key removal or storage behavior.
{% endhint %}

If you still need support after this page, share your framework, inventory, start order, and whether you are using item-based keys when asking for help.
