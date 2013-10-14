# TouchMonitor

The final program can be found in [demos/touchmonitor](../demos/touchmonitor)

This demo is very similar to [docs/TouchTerm.md](./TouchTerm.md), but this time we will use 2 Advanced Monitors to draw on.


## Setup

1 Advanced Computer, 2 Advanced Monitors (width 4, height 3), 3 Wired Modems (attached to the computer and the monitors) and some Networking Cable to connect the modems. Right-clicking the modems attached to the monitors turns them red and shows their name like "Peripheral monitor_0 connected.". We will use this name later on to wrap this monitor and acquire its term.

## Getting the terminals

Just wrap the connected monitors and get a viewport for each of them.

```lua
viewportLeft = viewportAPI.new(peripheral.wrap("monitor_0"))
viewportRight = viewportAPI.new(peripheral.wrap("monitor_1"))
```

## Drawing the buttons

This is nearly the same as in [docs/TouchTerm.md](./TouchTerm.md). We just assign the buttons to different viewports:
```lua
viewportLeft:addElement(buttonUp)
viewportLeft:addElement(buttonDown)
viewportRight:addElement(buttonLeft)
viewportRight:addElement(buttonRight)

viewportLeft:addElement(testbtn)
viewportRight:addElement(testbtn)
```

## The button callback handler

This is nearly the same as in [docs/TouchTerm.md](./TouchTerm.md). We just call `move(dx, dy)` for both viewports within the `handler` function:
```lua
handler = function(element, x, y)
	[...]
	viewportLeft:move(dx, dy)
	viewportRight:move(dx, dy)
	return true
end
```

## The event dispatcher

Register an event handler for `monitor_touch` events for each monitor and register a `monitor_resize` handler for both of them, too. And finally run the dispatch loop.
```lua
eventDispatcherAPI.addFilteredHandler("monitor_touch", "monitor_0", function(event, side, xPos, yPos)
	redraw = viewportLeft:handleClick(xPos, yPos)
	if redraw then
		viewportRight:redraw()
	end
end)
eventDispatcherAPI.addFilteredHandler("monitor_touch", "monitor_1", function(event, side, xPos, yPos)
	redraw = viewportRight:handleClick(xPos, yPos)
	if redraw then
		viewportLeft:redraw()
	end
end)

eventDispatcherAPI.addFilteredHandler("monitor_resize", "monitor_0", function()
	viewportLeft:redraw()
end)
eventDispatcherAPI.addFilteredHandler("monitor_resize", "monitor_1", function()
	viewportRight:redraw()
end)

eventDispatcherAPI.runDispatchLoop()
```
