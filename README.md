<div align="center">

![Project Logo](Images/Relay-Logo.png)

<div align="left">

# What is Relay?
Relay is a powerfull communication module that allows you to pass on information from one script to another

## Example code:
```lua
local Relay = require(script.Relay)

local key1 = "UpdateScore"
local key2 = "UpdatePlayerData"
----------------------------------


Relay:on(key1, function(player: Player, score: number)
	print(score)
end)

Relay:on(key2, function(player: Player, tbl: {cash: number, wins: number})
	print(tbl)
end)

--

Relay:middleware(key1, function(params: {any})
	print(`{params[1]} has {params[2]} score!`)
end)

--

Relay:fire(key1, "Player1", 1000)
Relay:fire(key1, "Player1", {50000, 136})
```
