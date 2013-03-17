# Elexx ComputerCraftAPI Collection

## Quick start

* copy `eventDispatcherAPI`, `touchScreenAPI` and `demos/touch` to your Advanced Computer
* attach an Advanced Monitor (min 2x3) to the right of your computer
* run `touch` on your computer

## APIs

At the moment there are the following APIs available:

### eventDispatcherAPI

This API allows you to register functions with will be called if a specific  [events](http://computercraft.info/wiki/Os.pullEvent#Event_types) occures.

```lua
-- var eventName - the event, e.g. "redstone"
-- var func      - a functionname, this function will be called if the given event occures
-- if two or more functions register to the same event,
-- there is no guarantee in which order they will be called.
eventDispatcherAPI.addHandler(eventName, func)

-- just waits until an event occurrence
-- and calls all registered callback functions for this event
eventDispatcherAPI.runDispatchLoop()
```

### touchScreenAPI

A simple API to draw buttons on a monitor and handle touch events.

#### Display

This is the most basic object, a representation of one attached Monitor

```lua
-- var side - the side where the monitor is attached to
-- returns display - a display object
touchScreenAPI.Display:create(side)

-- resets the display to default values, and whipes the screen
-- text color: white
-- background color: black
display:resetAndClear()

-- var button - a button object
display:addButton(button)

-- call this function with click position. it will find buttons
-- on this position and invoke their callback function
-- var xPos - x position
-- var yPos - y position
display:handleEvent(xPos, yPos)
```

#### Button

A button which is clickable.

```lua
-- var width, height - optional parameter
-- returns button    - a button object
Button:create(text, x, y, width, height)

-- changes the colors of the button, dont forget to redraw the button!
button:setColors(textColor, backgroundColor)

-- adds an function which will be called by display:handelEvent in case the button is touched
button:addListener(func)

-- draws the button on the given terminal (see display.term)
button:draw(term)
```

#### Rectangle

Just a plain rectangle.

```lua
Rectangle:create(x, y, width, height)
rectangle:setBackgroundColor(backgroundColor)
rectangle:draw(term)
```

