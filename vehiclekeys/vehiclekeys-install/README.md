---
description: Install Guide
icon: wrench
---

# Install

Start Order Must be after the inventory you use and ox\_lib.

If the garage you use uses autodetect must be before the garage.

This is because many scripts (including my own use autodetect to check if a resource is running)

Here is an example

```
ensure ox_lib
ensure example_famework_name
ensure example_inventory_name
ensure MrNewbVehicleKeys
ensure example_garage_name
```

Please note, this is an example. Please do not put this in your config file like this.
