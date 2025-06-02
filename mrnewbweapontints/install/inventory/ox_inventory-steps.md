# ox\_inventory Steps

Add this to ox\_inventory/data/items.lua



```lua
['newbserialfile'] = { 
	label = 'Heavy File',
	stack = false,
	close = true,
	allowArmed = true,
	weight = 10,
	server = {
		export = 'MrNewbWeaponTints.newbserialfile'
	},
	consume = 0.50
},

['greentint'] = { 
	label = 'Green Weapon Tint',
	stack = false,
	close = true,
	allowArmed = true,
	weight = 10,
	server = {
		export = 'MrNewbWeaponTints.setweapontint',
		tint = 1
	}
},

['goldtint'] = { 
	label = 'Gold Weapon Tint',
	stack = false,
	close = true,
	allowArmed = true,
	weight = 10,
	server = {
		export = 'MrNewbWeaponTints.setweapontint',
		tint = 2
	}
},

['pinktint'] = { 
	label = 'Pink Weapon Tint',
	stack = false,
	close = true,
	allowArmed = true,
	weight = 10,
	server = {
		export = 'MrNewbWeaponTints.setweapontint',
		tint = 3
	}
},

['armytint'] = { 
	label = 'Army Weapon Tint',
	stack = false,
	close = true,
	allowArmed = true,
	weight = 10,
	server = {
		export = 'MrNewbWeaponTints.setweapontint',
		tint = 4
	}
},

['lspdtint'] = { 
	label = 'LSPD Weapon Tint',
	stack = false,
	close = true,
	allowArmed = true,
	weight = 10,
	server = {
		export = 'MrNewbWeaponTints.setweapontint',
		tint = 5
	}
},

['orangetint'] = { 
	label = 'Orange Weapon Tint',
	stack = false,
	close = true,
	allowArmed = true,
	weight = 10,
	server = {
		export = 'MrNewbWeaponTints.setweapontint',
		tint = 6
	}
},

['platinumtint'] = { 
	label = 'Platinum Weapon Tint',
	stack = false,
	close = true,
	allowArmed = true,
	weight = 10,
	server = {
		export = 'MrNewbWeaponTints.setweapontint',
		tint = 7
	}
},
```
