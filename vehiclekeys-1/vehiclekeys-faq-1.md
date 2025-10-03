---
description: Heres a list of available commands in the script.
icon: message-smile
---

# Commands





## Admin Commands

*   [ ] /giveadminkey

    ```
    This command will require you to pass a id and a plate for the key you wish to grant

    -- example
    -- /giveadminkey 1 MYCOLPL8
    -- this would give keys to player 1 for MYCOLPL8
    ```
*   [ ] /givenearbykey

    ```
    This command will give keys to the closest vehicle in range
    ```
* [ ] /vehiclekeyAdmin

***



## Player Commands

1.  /proximitylocks

    ```
    This will enable or disable the proximity locking prefrence for the player.
    -- Proximity locks must be enabled for this to be work
    ```
2.  /lockvehicle

    ```
    This will toggle the lock to the closest vehicle, this is also a keybound command
    available by pressing l by defualt
    --this can be rebound at Config.KeybingSettings.LockKeyBind
    ```
3.  /enginetoggle

    ```
    This will toggle the engine of the car a player is sitting in, this is also a keybound command 
    available by pressing g by defualt
    -- Engine toggle must be enabled in the config for this to work and can be changed in Config.KeybingSettings.EngineKeyBind
    ```
4.  /keyring

    ```
    This command is only enabled when using non item based and will show all current keys
    held by the player, also offers sub menus to give keys etc
    ```
5.  /givekeys

    ```
    This command is only enabled when using non item based and will give keys to the
    closest car to the closest player
    -- This will only give the keys if the player actually has them
    ```
6.  /fob

    ```
    This command is only enabled when using non item based and will pull up the
    keyfob ui to the closest vehicle (or vehicle ped is in) as long as the player has the keys
    ```
