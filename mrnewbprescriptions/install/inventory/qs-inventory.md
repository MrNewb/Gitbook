---
description: Inventory Install Steps
icon: box-circle-check
---

# qs-inventory

Add this to qs-inventory/config/metadata.js, This edit will add the description when you hover over the item

```javascript
} else if (itemData.name == "medicalprescription") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
} else if (itemData.name == "zombix") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
} else if (itemData.name == "willies") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
} else if (itemData.name == "mollis") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
} else if (itemData.name == "realquickioum") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
} else if (itemData.name == "naptimeioum") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
} else if (itemData.name == "rumaierum") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
} else if (itemData.name == "stretchyioum") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
} else if (itemData.name == "jimmyioum") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
} else if (itemData.name == "crowlyioum") {
    $(".item-info-title").html("<p>" + `${itemData.info.label || label}` + "</p>");
    $(".item-info-description").html("<p>" + itemData.info.description+ "</p>");
```



* Next drag the images from the install folder into the inventory image folder.
