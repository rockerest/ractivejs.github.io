# Known issues, FAQs, and Tips


## Known Issues

### Memory and crashing issues with Safari on iOS 9

It seems that Apple has introduced some memory management _feature_ with Safari in iOS 9 that causes large templates to crash Safari during parsing. Fortunately, this can be worked around by splitting your templates into smaller partials or, more efficiently, by pre-parsing your templates and serving them as a JS object. You can use [Ractive.parse()](Ractive.parse().md) to create the JS object as a build step or when the page is being served.

iOS 8 seems to remain unaffected.

## FAQs

__Coming Soon!&tmp;__

## Tips

### Using Ractive with...

* [...Backbone](using-ractive-with-backbone.md)
* [...RequireJS](using-ractive-with-requirejs.md)
* [...Browserify](using-ractive-with-browserify.md)
* [...Yeoman](using-ractive-with-yeoman.md)
* [...built-in Promise support](Promises.md)
* [...jQuery Mobile](using-ractive-with-jquery-mobile.md)
<!-- TODO * [...Underscore (and other utility libraries)](using-ractive-with-underscore) -->

### Building an app with Ractive

Ractive can take care of your UI, and for simple applications it can take care of your *application state* as well. But if you're building a complex app you'll likely have other things to worry about as well - routing and history management, fetching and saving data to and from a server, validating data, handling realtime communication, user authentication, and all the other fun stuff that goes into a web app.

Unlike mega-frameworks like Angular and Ember, Ractive doesn't have an opinion about these things - you're encouraged to build your app from loosely coupled modules. It means you're not beholden to a particular framework's way of doing things, and you can swap out (for example) your routing library for something better later on, but it does mean that you're now responsible for making those decisions.

This section is designed to help with that, by collecting tips and advice. If you think your experience can help other developers, please add it to the wiki!

* [Routing](Routing.md)
