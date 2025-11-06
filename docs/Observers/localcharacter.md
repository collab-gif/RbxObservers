# Local Character

Use the `observeLocalCharacter` observer to observe the lifespan of the local character.
This can only be run on the client.

```lua
Observers.observeLocalCharacter(function(character)
	print("Local character has spawned")
	return function()
		print("Local character has been removed")
	end
end)
```
