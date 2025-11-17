---
description: Install Guide
icon: wrench
---

# Install

Start Order Must be after the inventory you use, ox\_lib, and community\_bridge.

This is because many scripts (including my own use autodetect to check if a resource is running)

Here is an example

```
ensure ox_lib
ensure example_famework_name
ensure example_inventory_name
ensure example_targetscript_name
ensure community_bridge
ensure MrNewbVehicleRentals
```

Please note, this is an example. Please do not put this in your config file like this.

[https://github.com/MrNewb/community\_bridge](https://github.com/MrNewb/community_bridge)
