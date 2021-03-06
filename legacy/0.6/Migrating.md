# 'Migrating to 0.6.x'


These migration notes are cribbed from the [CHANGELOG](https://github.com/ractivejs/ractive/blob/dev/CHANGELOG.md). While we strive to minimise breaking changes, and to highlight the ones we do introduce, if you discover an undocumented breaking change please edit this page.

## Migrating from 0.5.x

### Lifecycle events

Ractive instances now emit *lifecycle events*. If you use `Ractive.extend(...)` with `init()`, `beforeInit()` or `complete()`, you will need to replace them - they will continue to work, but will be removed in a future version.

`init()` can be replaced with one of the following methods, or you may need to split your code into both methods. Use `onrender()` for code that needs access to the rendered DOM, but is safe being called more than once if you unrender and rerender your ractive instance. Use `oninit()` for code that should run only once or needs to be run regardless of whether the ractive instance is rendered into the DOM.

The `init()` method also no longer recieves an `options` parameter as the ractive instance now inherits _all_ options passed to the constructor. You can still access the options directly using the `onconstruct()` method.

`beforeInit()` and `complete()` can be replaced directly with `onconstruct()` and `oncomplete()` respectively.

See the [lifecycle events](lifecycle events.md) page for more detail.

### Other Breaking changes

* `new Ractive()` now inherits all options as methods/properties including event hooks. If you have been passing data through custom initialisation options be aware that they will appended to your ractive instance.
* Using other elements besides `<script>` for templates is an now an error. Migrate any templates in non-script elements and include a non-javascript type so the browser does not try to interpret your template:

	```js
		<script id='template' type='text/ractive'>
			Your template goes here
		</script>
	```

* New reserved events cannot be used for proxy event names, i.e. `<p on-click='init'></p>`. These include 'change', 'config', 'construct', 'init', 'render', 'reset', 'teardown', 'unrender', and 'update'. You will need to rename your events.
* Setting uninitialised data on a component will no longer cause it to leak out into the parent scope
* 'Smart updates', via `ractive.merge()` and `ractive.shift()` etc, work across component boundaries. In most cases this is the expected behavior.
* The CSS length interpolator has been removed.


## Migrating from 0.4.x

### Breaking changes

* Errors in observers and evaluators are no longer caught
* Nodes are detached as soon as any outro transitions are complete (if any), rather than when *all* transitions are complete
* (Outdated if you are moving to `0.6.x` or above) The options argument of `init: function(options)` is now strictly what was passed into the constructor, use `this.option` to access configured value.
* `data` with properties on prototype are no longer cloned when accessed. `data` from "baseClass" is no longer deconstructed and copied.
* Options specified on component constructors will not be picked up as defaults. `debug` now on `defaults`, not constructor
* Select bindings follow general browser rules for choosing options. Disabled options have no value.
* Input values are not coerced to numbers, unless input type is `number` or `range`
* `{{this.foo}}` in templates now means same thing as `{{.foo}}`
* Rendering to an element already render by Ractive causes that element to be torn down (unless appending).
* Illegal javascript no longer allowed by parser in expressions and will throw
* Parsed template format changed to specify template spec version.
	* Proxy-event representation
	* Non-dynamic (bound) fragments of html are no longer stored as single string
	* See https://github.com/ractivejs/template-spec for current spec.
* Arrays being observed via `array.*` no longer send `item.length` event on mutation changes
* Reserved event names in templates ('change', 'config', 'construct', 'init', 'render', 'reset', 'teardown', 'unrender', 'update') will cause the parser to throw an error
* `{{else}}` support in both handlebars-style blocks and regular mustache conditional blocks, but is now a restricted keyword that cannot be used as a regular reference
* Child components are created in data order
* Reference expressions resolve left to right and follow same logic as regular mustache references (bind to root, not context, if left-most part is unresolved).
* Improved attribute parsing and handling:
	* character escaping and whitespace handling in attribute directive arguments
	* boolean and empty string attributes
* Computed properties no longer create nested objects with keypath like names, i.e. `page.area: '${width} * ${height}'` creates a property accessible by `{{page.area}}` but not `{{#page}}{{area}}{{/page}}`
* The element into which the ractive instance was rendered is no longer available as `ractive.el`. See [ractive.render()](ractive.render().md) and [ractive.insert()](ractive.insert().md) for more information on moving ractive instances in the DOM.
