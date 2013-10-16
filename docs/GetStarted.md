# Get Started

The final program can be found in [demos/get_started](../demos/get_started)

## Draw a button

First of all, copy the apis to your computer and load the apis with `os.loadAPI()`

Create a new viewport:

```lua
viewport = viewportAPI.new({term = term})
```

where `term` can be the default term which resolves to the current computer screen or any wrapped peripheral which provides a terminal.

Next create a simple button

```lua
button = buttonAPI.new({
	x = 1, y = 1, width = 10, height = 1
})
```

`x`, `y`, `width` and `height` is the bare minimum of arguments which must be set.

Now add the button to the viewport and redraw it.

```lua
viewport:addElement(button)
viewport:redraw()
```

If you run the program right now you will see a white square on the top left of your screen, this is the button we created!

## Make it clickable

But what about some fancy clicky clicky stuff?
Well, first of all a function is needed which will be called if the button is clicked.

```lua
function clickHandler(element, posX, posY)
	element.backgroundColor = element.backgroundColor == colors.white and colors.green or colors.white
	return true
end
```

this function toggles the background color of a given element from white to green and back each time it gets called. The `return true` forces a redraw of the viewport.

next the function needs to be hooked in

```lua
button.callback = clickHandler
```

of course this could have been done right in `buttonAPI.new({ ..., callback = clickHandler})` provided the function has already declared then.

and finally we need a event handling system like this

```lua
while true do
	event, side, xPos, yPos = os.pullEvent("mouse_click")
	viewport:handleClick(xPos, yPos)
end
```

Run the program and click the button :)
