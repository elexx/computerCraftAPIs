# ViewportAPI Documentation

* `viewportAPI.new({})` returns a new viewport. parameters are provided as a table:
* `term` the terminal which will be managed by the new viewport - required
* `textColor` the default text color - defaults to white
* `backgroundColor` the default background color - defaults to black

## Methods

* `viewport:move(x, y)` moves the panel behin the viewport.
* `viewport:setPosition(x, y)` set the panels position, i.e. an absolute movement
* `viewport:addElement(element)` adds an element, e.g. a button created by the [buttonAPI](../buttonAPI) ([docs](./ButtonAPI.md))
* `viewport:handleClick(xPos, yPos)` calls the callback function of every element at the given position
* `viewport:redraw()` redraws all element on this viewport

## Structur of `element`

An element has to have:
* `x`, `y`, `width`, `height` as either a number or a function which takes 2 arguments: the terms height and width and returns a number. e.g. `function x(self, termx, termy) return termx / 2 end`

An element can have:
* `draw(term, offsetX, offsetY)` a function which draws the button on the given terminal in respect to the backpanel offset
* `isSticky` a boolean (if it is missing it counts as false). True if the element is on the viewport, false if it's on the backpanel.
* `callback(element, xPos, yPos)` a function which will be called if the button occupies the clicked coordinates. `element` is the element itself, _Pos are the clicked coordinates. Should return `true` if a redraw after its call is needed.

## Example

```lua
viewport = viewportAPI.new(term)
viewport:addElement(someButton)
viewport:redraw()
```
