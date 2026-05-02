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

---

You can communicate between different scripts:

## Example 1

### Script 1
```lua
local Relay = require(script.Parent.Relay)

task.wait() -- To make sure that the listener has loaded first.

Relay:fire("ReceiveMessage", "Hello from the another script!!")
```

### Script 2
```lua
local Relay = require(script.Parent.Relay)

Relay:on("ReceiveMessage", function(message: string)
	print("Received message:", message)
end)
```

## Example 2

### Script 1
```lua
local Relay = require(script.Parent.Relay)

task.wait() -- To make sure that the listener has loaded first.

local money = Relay:request("Money", 100, 1000) -- Key, Min, Max
print(money)
```

### Script 2
```lua
local Relay = require(script.Parent.Relay)

Relay:handleRequest("Money", function(min: number, max: number)
	return math.random(min, max)
end)
```
