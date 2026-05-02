---
description: These are edits required for qb-inventory
icon: q
---

# qb-inventory

This edit adds a metadata tooltip to the `vehiclekeys` item so players can see the vehicle name and plate when hovering over the key in their inventory.

{% embed url="https://github.com/qbcore-framework/qb-inventory/blob/be813ebe73287da7277f1c9589a03f7de213f976/html/js/app.js#L356" %}
Go to this line in qb-inventory/html/js/app.js
{% endembed %}

Find the `switch` block that handles item display and add a new `case` for `vehiclekeys`:

```javascript
case "vehiclekeys":
    return `<p><strong>Vehicle Keys for </strong><span>${itemData.info.vehName}</span></p>
    <p><strong>Plate # </strong><span>${itemData.info.plate}</span>`;
```
