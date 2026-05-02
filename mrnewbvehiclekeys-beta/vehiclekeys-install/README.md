---
description: Install Guide
icon: wrench
---

# Install

This guide gets the base resource running in the right order before you move on to framework hooks, inventory items, and gameplay tuning.

## Before You Start

You only need to do four things to get the script online:

1. Set the correct resource start order.
2. Follow the framework guide for your core.
3. Add the required inventory items and images.
4. Review the configuration guide, then test the full vehicle flow before going live.

If you are already comfortable with your framework and inventory setup, this page should be quick.

## Step 1: Start Order

MrNewbVehicleKeys must start **after** your inventory, target, ox\_lib, and community\_bridge resources. Many scripts, including this one, use auto-detection to check if a resource is running, so start order matters.

{% hint style="warning" %}
This is an example only. Adjust the resource names to match what you actually have installed.
{% endhint %}

```ini
ensure ox_lib
ensure <your_framework>         # e.g. qb-core, es_extended, qbx_core
ensure <your_inventory>         # e.g. ox_inventory, qb-inventory
ensure <your_target>            # e.g. ox_target, qb-target
ensure community_bridge
ensure MrNewbVehicleKeys
ensure <your_garage>            # e.g. qb-garages, ox_garage
```

**community\_bridge** is required: [https://github.com/MrNewb/community\_bridge](https://github.com/MrNewb/community_bridge)

<figure><img src="../../.gitbook/assets/install.gif" alt="Example resource folder layout showing community_bridge and MrNewbVehicleKeys in the server resources directory."><figcaption><p>Example resource layout showing <code>community_bridge</code> and <code>MrNewbVehicleKeys</code> placed in your resources folder before you sort out final start order.</p></figcaption></figure>

## Step 2: Framework Setup

Open the framework guide that matches your server core and complete that first:

* `esx`
* `qb-core`
* `qbox`

Do not move on until the correct framework bridge and required items are in place.

## Step 3: Inventory Setup

After the framework side is done, add the correct inventory items and images for your inventory system.

This is the step that usually causes missing item, missing image, or unusable key issues if it gets skipped.

## Step 4: First Test

Before you start tuning config values, test one basic workflow from start to finish:

1. Spawn or retrieve a vehicle.
2. Confirm you have access.
3. Lock and unlock it.
4. Confirm keys can be granted, removed, or stored the way you expect.

{% hint style="success" %}
If the basic workflow works here, the rest of setup usually becomes much easier.
{% endhint %}

## Step 5: Configuration

After the base install is working, use the [Configuration Guide](configuration.md) to tune gameplay, pricing, keyring behavior, dispatch, and shared key storage. It also covers the optional `provide` aliases in `fxmanifest.lua` for migration setups.

If you still need support after this page, share your framework, inventory, start order, and whether you are using item-based keys when asking for help.
