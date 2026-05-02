---
description: Practical examples showing how to integrate MrNewbVehicleKeys with other scripts.
icon: scissors
---

# Snippet Examples

{% hint style="info" %}
These snippets show the minimum changes needed to add key support to common scripts. You should adapt them to match your own version of each resource.
{% endhint %}

## Use This Section When...

Use the snippet pages when a resource does not already have built-in MrNewbVehicleKeys support and you need a practical example of where to add give-key or remove-key calls.

{% hint style="success" %}
If a script already includes a native key-system option, prefer that config route first. Use code snippets only when the integration has to be patched manually.
{% endhint %}

## Snippet Index

| Resource | Best use case |
| --- | --- |
| [qb-garages](qb-garages.md) | Give keys on garage takeout and remove them on cleanup or delete |
| [qb-vehicleshop](qb-vehicleshop.md) | Handle test drive keys and purchased vehicle keys |
| [qbx_adminmenu](qb-vehicleshop-1.md) | Replace hardcoded Qbox key export calls in admin vehicle spawning |
| [jg-advancedgarage](jg-advancedgarage.md) | Use a native config option instead of patching code |
| [jg-dealerships](jg-dealerships.md) | Use a native config option instead of patching code |
| [wasabi_bridge](wasabi_bridge.md) | Route bridge-based key actions through MrNewbVehicleKeys |

{% hint style="warning" %}
Always test the full workflow after applying a snippet: spawn or retrieve the vehicle, confirm keys are granted, then confirm they are removed or cleaned up at the correct time.
{% endhint %}

{% hint style="info" %}
If your script is not listed here, bring the relevant spawn, store, sale, rental, or cleanup code into the support Discord and it becomes much easier to point you at the right MrNewbVehicleKeys export pattern.
{% endhint %}
