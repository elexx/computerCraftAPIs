# TouchTerm

The final program can be found in [demos/touchterm](../demos/touchterm)

This demo shows how to draw sticky and none-sticky buttons, how to move the backpanel, how to use callbacks for button positioning and size and how to use the event dispatcher.

## Draw the buttons

```lua
buttonUp = buttonAPI.new({
	text = "up",
	x = buttonAPI.anchorLeft,
	y = buttonAPI.anchorTop,
	isSticky = true,
	width = buttonAPI.maxWidth,
	height = 1
})
```

Creates a new button, with the label "up", a x position on the left side of the screen, y on top, it will stick there even if the backpanel is moved, the width is set to maximum screen width and it's height is 1. The other 3 movement buttons are created in a similar manner.

The moveable, non-sticky button gets a `isSticky = false` and in addition a background color, which will be toggled if the button is clicked.

## The button callback handler

This function serves as callback function for all 4 movement buttons. It moves the viewport on x or y according to the clicked button. In addition it toggles the color of the testbtn and requests a redraw of our viewport (`return true`).

```lua
handler = function(element, x, y)
	dx = 0
	dy = 0
	if element == buttonUp then
		dy = -1
	elseif element == buttonDown then
		dy = 1
	elseif element == buttonLeft then
		dx = -1
	elseif element == buttonRight then
		dx = 1
	elseif element == testbtn then
		testbtn.backgroundColor = testbtn.backgroundColor == colors.green and colors.red or colors.green
	else
		error("Unknown Button")
	end
	viewport:move(dx, dy)
	return true -- requests redraw of current viewport
end
```

## The event dispatcher

Finally we register a callback to the `mouse_click` event, which gets queued if one clicks the computer terminal and run the dispatch loop.

```lua
eventDispatcherAPI.addHandler("mouse_click", function(event, side, xPos, yPos)
	viewport:handleClick(xPos, yPos)
end)

eventDispatcherAPI.runDispatchLoop()
```

