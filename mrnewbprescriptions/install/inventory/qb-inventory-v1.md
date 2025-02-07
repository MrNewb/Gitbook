---
description: Inventory Install Steps
icon: box-circle-check
---

# qb-inventory V1

{% embed url="https://github.com/qbcore-framework/qb-inventory/blob/be813ebe73287da7277f1c9589a03f7de213f976/html/js/app.js#L356" %}
Go to this line and add this in qb-inventory/html/js/app.js
{% endembed %}

Add a new "case" under any of the others already listed and paste this in.

```javascript
    case "medicalprescription":
        return `<p><strong>Prescription: </strong><span>${itemData.info.description}</span></p>`;
    case "zombix":
        return `<p><strong>Prescription: </strong><span>${itemData.info.description}</span></p>`;
    case "willies":
        return `<p><strong>Prescription: </strong><span>${itemData.info.description}</span></p>`;
    case "mollis":
        return `<p><strong>Prescription: </strong><span>${itemData.info.description}</span></p>`;
```
