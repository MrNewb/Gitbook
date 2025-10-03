---
description: These are edits required for ps-inventory
icon: fork
---

# ps-inventory

{% hint style="info" %}
[https://github.com/Project-Sloth/ps-inventory/blob/27b0ebe84c672bcf0d8e1cbc0ff54ca1f3caebec/html/js/app.js#L621](https://github.com/Project-Sloth/ps-inventory/blob/27b0ebe84c672bcf0d8e1cbc0ff54ca1f3caebec/html/js/app.js#L621)

Using the above as an example, on where to put this
{% endhint %}

Add a new "else if" under any of the others already listed and paste this in.

```javascript
} else if (itemData.name == "vehiclekeys") {
      $(".item-info-title").html("<p>" + itemData.label + "</p>");
      $(".item-info-description").html('<p><strong>Vehicle Keys for:  </strong><span>' + itemData.info.vehName + "</p><p style=\"font-size:11px\"><b>Plate: </b>" + itemData.info.plate + "</a>");
```
