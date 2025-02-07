---
description: >-
  This is a example of the CreatePrescription export, this will allow you to add
  the data to items via metadata that can be used and have effects.
icon: cannabis
---

# qb-drugs

```lua
local function givePrescriptionMed(src)
    local random = math.random(1,100)
    local luck = 50
    if random >= luck then return end
    local meds = {
	name = 'zombix',
	usableitem = 'zombix',
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
    exports.MrNewbPrescriptions:CreatePrescription(src , meds)
end

RegisterNetEvent('qb-drugs:server:giveStealItems', function(drugType, amount)
    local src = source
    local Player = QBCore.Functions.GetPlayer(src)
    if not Player or StolenDrugs == {} then return end
    for k, v in pairs(StolenDrugs) do
        if drugType == v.item and amount == v.amount then
            givePrescriptionMed(src)
            exports['qb-inventory']:AddItem(src, drugType, amount, false, false, 'qb-drugs:server:giveStealItems')
            table.remove(StolenDrugs, k)
        end
    end
end)
```
