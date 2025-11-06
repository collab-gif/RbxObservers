# Characters

Use the `observeCharacter` observer to observe the lifespan of characters in the game.

```lua
Observers.observeCharacter(function(player, character)
	-- Character was spawned
	print("Character spawned for " .. player.Name)

	-- Wait for humanoid:
	local humanoid = character:WaitForChild("Humanoid", 60)

	-- Listen to humanoid Died event:
	local onDiedConn: RBXScriptConnection? = nil
	if humanoid then
		onDiedConn = humanoid.Died:Connect(function()
			print("Character died for " .. player.Name)
		end)
	end

	return function()
		-- Character was removed
		print("Character removed for " .. player.Name)
		if onDiedConn then
			onDiedConn:Disconnect()
			onDiedConn = nil
		end
	end
end)
```

There are scenarios where you only want to observe characters from a select list of players.
This can be done by providing a list of players as the final argument to `observeCharater`:

```lua
Observers.observeCharacter(function(player, character)
	...
end, { somePlayer, anotherPlayer }) -- Only observe characters from 'somePlayer' and 'anotherPlayer'
```
