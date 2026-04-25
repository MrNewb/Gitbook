---
description: These are edits required for ps-inventory
icon: fork
---

# ps-inventory

This edit adds a metadata tooltip to the `vehiclekeys` item so players can see the vehicle name and plate when hovering over the key in their inventory.

{% hint style="info" %}
Use the link below as a reference for where to insert the code — find the block that handles item tooltips and add the new `else if` alongside the existing ones.

[https://github.com/Project-Sloth/ps-inventory/blob/27b0ebe84c672bcf0d8e1cbc0ff54ca1f3caebec/html/js/app.js#L621](https://github.com/Project-Sloth/ps-inventory/blob/27b0ebe84c672bcf0d8e1cbc0ff54ca1f3caebec/html/js/app.js#L621)
{% endhint %}

```javascript
} else if (itemData.name == "vehiclekeys") {
    $(".item-info-title").html("<p>" + itemData.label + "</p>");
    $(".item-info-description").html('<p><strong>Vehicle Keys for:  </strong><span>' + itemData.info.vehName + "</p><p style=\"font-size:11px\"><b>Plate: </b>" + itemData.info.plate + "</a>");
```
