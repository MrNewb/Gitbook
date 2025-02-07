---
description: >-
  This is a example of the medical insurance, this will allow you to get if a
  player is insured and then if so give them a discounted revive cost. This
  export can be used however you wish.
icon: hospital
---

# qbx\_ambulancejob

```lua
local function billPlayer(src)
	local player = exports.qbx_core:GetPlayer(src)
	local price = exports.MrNewbPrescriptions:ReturnInsuredRate(src, sharedConfig.checkInCost)
	print("Original Price: "..sharedConfig.checkInCost)
	print("New Price: "..price)
	player.Functions.RemoveMoney('bank', price, 'respawned-at-hospital')
	config.depositSociety('ambulance', price)
	TriggerClientEvent('hospital:client:SendBillEmail', src, price)
end
```
