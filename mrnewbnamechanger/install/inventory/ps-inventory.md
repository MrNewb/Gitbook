---
icon: fork
---

# ps-inventory

### ps-inventory Edit for Metadata/Info Display on Hover

On line 647 of [ps-inventory](https://github.com/Project-Sloth/ps-inventory/blob/d8e99de867b2b6d49186f707548c4f4ecde201ab/html/js/app.js#L647), add the following line:

```javascript
    } else if (itemData.name == "filledcertificate") {
        $(".item-info-title").html("<p>" + itemLabel + "</p>");
        $(".item-info-description").html(
            "<p><strong>First Name: </strong><span>" +
            itemData.info.firstname +
            "</span></p><p><strong>Last Name: </strong><span>" +
            itemData.info.lastname +
            "</span></p>"
        );
    }
```
