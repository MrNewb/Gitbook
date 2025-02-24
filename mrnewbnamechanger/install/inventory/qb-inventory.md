---
icon: q
---

# qb-inventory

### Qb-inventory Edit for Metadata/Info Display on Hover

On line 362 of [qb-inventory](https://github.com/qbcore-framework/qb-inventory/blob/c8b7ffb910c41bdff619ac23281bfbe1b927e64b/html/js/app.js#L362), add the following line:

```javascript
case "filledcertificate":
    return `<p><strong>First Name: </strong><span>${itemData.info.firstname}</span></p>
    <p><strong>Last Name: </strong><span>${itemData.info.lastname}</span></p>`;
```
