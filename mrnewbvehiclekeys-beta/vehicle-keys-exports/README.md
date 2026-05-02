---
icon: file-export
---

# Exports

Exports let other resources interact with MrNewbVehicleKeys directly. They are the recommended way to integrate with this script.

{% hint style="info" %}
If you are migrating from **qb-vehiclekeys**, the [backwards-compatible events](../backwards-events/README.md) are also supported, but using exports gives you access to additional features.
{% endhint %}

## What Exports Are For

Use exports when another script needs to talk to MrNewbVehicleKeys directly.

- Server exports are useful when another resource needs to manage keys, ownership checks, rentals, or other shared vehicle access logic.
- Client exports are useful when another resource needs to interact with the local player's vehicle access features, keyfob actions, or convenience functions.
- Events are available for backwards compatibility if you are migrating older integrations and do not want to refactor everything immediately.

{% hint style="info" %}
If you are using item-based keys, some give-key exports support optional arguments like `autoKeyring`, and some remove-key exports support options like `deepSearch`. Those are documented on the dedicated reference pages below.
{% endhint %}

## Where To Go Next

| Page | Use It For |
|---|---|
| [Server Exports](server-exports.md) | Full server-side export list and usage details |
| [Client Exports](client-exports.md) | Full client-side export list and usage details |
| [Backwards-Compatible Events](../backwards-events/README.md) | Legacy event-based integrations and migration support |

