---
description: These are edits required for origen_inventory to work with vehiclekeys
icon: user-beard-bolt
---

# origen\_inventory

Add a new displayMeta in origen\_inventory\html\js\items.js

```javascript
displayMeta('vehiclekeys', (itemData, setTitle, setDescription) => {
    setDescription(`
        <p><strong>Vehicle Keys for a: </strong><span>${itemData.metadata.vehName}</span></p>
        <p><strong>Plate: </strong><span>${itemData.metadata.plate}</span></p>
    `);
})
```

To Add the vehiclekeys item if using ESX go into origen\_inventory\config\items.lua and add this item underneath one of the others. If using QB Core Follow Steps in the framework section and skip this part.

```
['vehiclekeys'] 		  = {['name'] = 'vehiclekeys', 	['label'] = 'Vehicle Keys', 	['weight'] = 100, 	    ['type'] = 'item', 		['image'] = 'vehiclekeys.png', ['unique'] = true, 	['useable'] = true, 	['shouldClose'] = true,	   ['combinable'] = nil,   ['description'] = 'Fancy vehicle keys'},
```
