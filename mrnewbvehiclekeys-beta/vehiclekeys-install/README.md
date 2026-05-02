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
4. Review the configuration guide and tune the features you want enabled.
5. Test spawning, locking, unlocking, and key granting before going live.

## Configuration

After completing the base install, review the [Configuration Guide](configuration.md). It documents the main `config.lua` sections, supporting config files, keyring behaviour, locksmith setup, dispatch, and job-based key storage via `KeyJobStorages`.

It also covers the optional `provide` aliases in `fxmanifest.lua` if you need MrNewbVehicleKeys to answer compatibility exports for older key-system resource names during migration.

{% hint style="info" %}
Use the install docs to get the script online first. Use the configuration guide after that to shape gameplay, pricing, keyring behavior, dispatch alerts, and job storage.
{% endhint %}

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

{% hint style="info" %}
If you still need support after this page, share your framework, inventory, start order, and whether you are using item-based keys when asking in Discord or opening a ticket.
{% endhint %}
