---
description: Inventory Install Steps
---

# 🐂 ox inventory

Add this to ox\_inventory/data/items.lua

```lua
	
	-- Start Of MrNewbPrescriptions
	["medicalprescription"] = {
		label = "medicalprescription",
		weight = 100,
		stack = false,
		close = true,
		description = "Medical Prescription",
		server = {
			export = 'MrNewbPrescriptions.medicalprescription'
		}
	},

	["prescriptionpad"] = {
		label = "prescriptionpad",
		weight = 100,
		stack = false,
		close = true,
		description = "Prescription Pad",
		server = {
			export = 'MrNewbPrescriptions.prescriptionpad'
		}
	},

	["zombix"] = {
		label = "zombix",
		weight = 100,
		stack = false,
		close = true,
		description = "Zombix 250 MG",
		server = {
			export = 'MrNewbPrescriptions.zombix'
		}
	},

	["willies"] = {
		label = "willies",
		weight = 100,
		stack = false,
		close = true,
		description = "Willies Butt Drain",
		server = {
			export = 'MrNewbPrescriptions.willies'
		}
	},

	["mollis"] = {
		label = "mollis",
		weight = 100,
		stack = false,
		close = true,
		description = "Mollis 50 MG",
		server = {
			export = 'MrNewbPrescriptions.mollis'
		}
	},
```

