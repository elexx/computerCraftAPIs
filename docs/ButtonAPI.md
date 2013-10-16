# ButtonAPI Documentation

## Textbox
`buttonAPI.newText({})` returns a new textbox. parameters are provided as a table:
* `x` and `y`: the strating position - required
* `width` and `height` of the textbox - required
* `text` the text displayed in the textpox - required
every parameter can be a function with the following signature `function(element, termx, termy)` where `termx` and `termy` are the size of the terminal.


## Button
`buttonAPI.new({})` returns a new button. parameters are provided as a table:
* `x` and `y`: the starting position - required
* `width` and `height` of the button - required
* `text`: the button label - defaults to ""
* `textColor`: the color of the label - defaults to black
* `backgroundColor`: the color of the backgroudn - defaults to white
* `isSticky`: if this button shall be drawn on the viewport or on the panel behind the viewport - defaults to false
* `isVertical`: if the text shall be printed vertical or horizontal - defaults to false
* `callback`: the callback function which will be called if the button is clicked - defaults to nil
every parameter can be a function with the following signature `function(element, termx, termy)` where `termx` and `termy` are the size of the terminal.


## Label
a label is basically a textbox which redirects clicks to an associated button
`buttonAPI.newLabel({})` returns a new label. parameters are provided as a table:
* `x` and `y`: the starting position - required
* `width` and `height` of the button - required
* `text` the text displayed in the textpox - required
* `button` a button - required
every parameter can be a function with the following signature `function(element, termx, termy)` where `termx` and `termy` are the size of the terminal.


## Helper functions and constants
* `buttonAPI.anchorTop` can be used as `x` to but a button on the first line on the terminal
* `buttonAPI.anchorBottom` can be used as `x` to but a button on the last line of the terminal
* `buttonAPI.anchorLeft` can be used as `y` to but a button on the first column of the terminal
* `buttonAPI.anchorRight` can be used as `y` to but a button on the last column of the terminal
* `buttonAPI.width(percent)` can be used as `width` to draw a button with `percent` of the screen width
* `buttonAPI.maxWidth` is an alias for `buttonAPI.width(1)` which gets a width of 100% of the screen width
* `buttonAPI.height(percent)` can be used as `heigth` to draw a button with `percent` of the screen height
* `buttonAPI.maxHeigh` is an alias for `buttonAPI.height(1)` which gets a height of 100% of the screen height


## Example
```lua
button = buttonAPI.new({
	x = 3,
	y = 1,
	width = buttonAPI.maxWidth,
	heigth = 2,
	text = "button",
	isSticky = true,
	textColor = colors.green
})
```
