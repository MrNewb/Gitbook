---
description: This is a list of the available server side exports.
---

# Server Exports

## GetInsurance

```lua
-- This export will return true/false based on insurance status of player

exports.MrNewbPrescriptions:GetInsurance(source)
```

## ReturnInsuredRate

```lua
-- This export will return a value based on if the source player has insurance or not
-- the amount could be a medical bill and then you could pass this and it will give
-- a price based on a player being insured or not

exports.MrNewbPrescriptions:ReturnInsuredRate(source, amount)
```

## CreatePrescription

```lua
-- This will give a prescription to the player
-- meds would be the value matching in config
-- these items have to exsist in the config but the values are adjustable in this
    local meds = {
		name = 'zombix',  
		usableitem = 'zombix', -- this item (anythign you want not owned by another script)  must be added to the config
		uses = 3,
		label = 'Zombix 250 MG',
		description = 'Zombix 250 MG',
		price = 500,
		icon = 'fa-solid fa-briefcase-medical',
		effect = 'stamina',
		value = 1.4,
		timecycle = 'drug_wobbly',
		strength = 0.56,
		time = 30,
	}
exports.MrNewbPrescriptions:CreatePrescription(source, meds)
```
