# ractive.shift()

The Ractive equivalent to ```Array.shift``` that removes an element from the beginning of the array at the given keypath and triggers an update event.

> ### ractive.shift( keypath )
> Returns a `Promise` (see [Promises](Promises.md)) that will resolve with the removed element after the update is complete.

> > #### **keypath** *`String`*
> > The [keypath](keypaths.md) of the array to change, e.g. `list` or `order.items`.

If the given keypath does not resolve to an array, an error will be thrown.
