# EventDispatcherAPI Documentation

The event dispatcher is designed to just exist once on a machine. There is no use of to dispatchers. Just register all callbacks to this dispatcher and start the dispatch loop.

## Methods

### addHandler
`eventDispatcherAPI.addHandler(eventName, func)` adds an handler for a given event name. There can be multiple handlers for one event name.

### setDefaultHandler
`eventDispatcherAPI.setDefaultHandler(func)` sets a handler to be called if no other handler exists and the event is not "terminate".

### queueEvent
`eventDispatcherAPI.queueEvent(eventName, param1, param2, param3)` just for the sake of completness, this is a wrapper to os.queueEvent(..)

### runDispatchLoop
`eventDispatcherAPI.runDispatchLoop()` fires up the event dispatcher

If an event gets queued:
* dispatcher fetches it and checks if there are any handlers interessted in this event and calls them one by one
* if no handler is registered, checks if is the "terminate" event, runDispatchLoop will return in this case
* if this is not the case and a default handler has been set, this one will be called
* otherwise the event will just be ignored

