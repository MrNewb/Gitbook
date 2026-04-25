---
icon: file-export
---

# Exports

Exports let other resources interact with MrNewbVehicleKeys directly. They are the recommended way to integrate with this script.

{% hint style="info" %}
If you are migrating from **qb-vehiclekeys**, the [backwards-compatible events](../backwards-events/README.md) are also supported, but using exports gives you access to additional features.
{% endhint %}

## Quick Reference

### Server Exports

| Export | Description |
|---|---|
| `GetPlayerKeys(src)` | Get all plates a player has keys for |
| `GiveKeys(src, netid)` | Give keys by vehicle network ID |
| `GiveKeysByPlate(src, plate)` | Give keys by plate string |
| `AddKeysByPlate(src, plate)` | Alias for GiveKeysByPlate |
| `HasKeys(src, netid)` | Check keys by network ID |
| `HasKeysByPlate(src, plate)` | Check keys by plate |
| `RemoveKeys(src, netid)` | Remove keys by network ID |
| `RemoveKeysByPlate(src, plate)` | Remove keys by plate |
| `TransferKey(src, targetSrc, plate)` | Transfer a key between players |
| `DuplicateKey(src, targetSrc, plate)` | Duplicate a key to another player |
| `UpdateKey(src, oldPlate, newPlate)` | Update a key after a plate change |
| `SetVehicleLock(netid, lockStatus)` | Lock/unlock a vehicle (1=unlock, 2=lock) |
| `RemoteLock(src, plate, lockStatus)` | Lock/unlock without vehicle being spawned |
| `VerifyOwnership(src, plate)` | Check if player owns the vehicle |
| `GetVehicleInfo(plate)` | Get stored vehicle data by plate |
| `GrantRental(src, plate, model, netid)` | Grant rental access |
| `RemoveRental(src, plate, netid)` | Remove rental access |
| `SetTempKey(src, plate, durationMs)` | Grant a timed temporary key |
| `RemoveTempKey(src, plate)` | Remove a temporary key |
| `SetTempKeyForPlayers(players, plate, ms)` | Grant temp key to multiple players |
| `RemoveTempKeyForPlayers(players, plate)` | Remove temp key from multiple players |
| `SetTempKeyForJob(job, plate, ms)` | Grant temp key to all players in a job |
| `RemoveTempKeyForJob(job, plate)` | Remove temp key from all players in a job |
| `KeyType()` | Returns true if item-based mode is on |
| `GetKeySystem()` | Returns the internal server system object |

### Client Exports

| Export | Description |
|---|---|
| `HasVehicleKeys(vehicle)` | Check if player has keys to a vehicle |
| `HaveKeys(vehicle)` | Alias for HasVehicleKeys |
| `HasKeysByPlate(plate)` | Check keys by plate |
| `GiveKeys(vehicle)` | Give local player keys by entity |
| `GiveKeysByPlate(plate)` | Give local player keys by plate |
| `RemoveKeys(vehicle)` | Remove local player keys by entity |
| `RemoveKeysByPlate(plate)` | Remove local player keys by plate |
| `GetPlayerKeyList()` | Get all plates player has keys for |
| `GetVehicleState()` | Check if player has keys to closest vehicle |
| `ToggleEngine(vehicle, forceState)` | Toggle or force vehicle engine state |
| `ToggleLock(vehicle)` | Toggle vehicle door lock |
| `IsVehicleHotwired(vehicle)` | Check if vehicle is hotwired |
| `SetVehicleHotwireImmune(vehicle, bool)` | Prevent/allow hotwiring |
| `SetVehicleLockpickImmuneEntity(v, bool)` | Prevent/allow lockpicking by entity |
| `SetVehicleLockpickImmunePlate(p, bool)` | Prevent/allow lockpicking by plate |
| `GetTempKey()` | Get global temp key bypass state |
| `SetTempKey(value)` / `ToggleTempKey(value)` | Set global temp key bypass |
| `SetTempKeyByPlate(plate, ms)` | Grant timed temp key by plate |
| `HasTempKey(plate)` | Check if player has a valid temp key |
| `RemoveTempKeyByPlate(plate)` | Remove temp key by plate |
| `DoesVehicleRequireKey(vehicle)` | Check if vehicle needs a key |
| `IsSharedJobVehicle(vehicle)` | Check if accessible via job |
| `CheckVehicleAccess(vehicle)` | Full access restriction check |
| `OpenKeyFob(plate, buttons)` | Open the keyfob UI |
| `StartVehicleAlarm(vehicle)` | Trigger vehicle alarm |
| `ToggleTrunk(vehicle)` | Open/close trunk |
| `ToggleRemoteStart(vehicle)` | Remote start engine |
| `DanceMode(vehicle)` | Trigger dance mode |
| `SelfParkVehicle(vehicle)` | Park at nearest parking spot |
| `SummonVehicle(vehicle)` | Drive vehicle to player |
| `ToggleAutoPilot(vehicle)` | Enable autopilot to GPS destination |
| `GetKeySystem()` | Returns the internal client system object |

