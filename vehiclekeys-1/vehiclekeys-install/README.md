---
description: Install Guide
icon: wrench
---

# Install

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
