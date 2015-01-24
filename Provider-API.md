The Provider API allows you to make autocomplete+ awesome. The Atom community will ultimately judge the quality of Atom's autocomplete experience by the breadth and depth of the provider ecosystem. We're so excited that you're here reading about how to make Atom awesome.

> The following examples are in CoffeeScript. If you would like to add JavaScript examples, please feel free to edit this page!

## Defining A Provider

You can create a provider by defining an object with the following properties:

* `selector` (required): Defines the scope selector(s) (can be comma-separated) for which your provider should receive suggestion requests
* `requestHandler` (required): Is called when a suggestion request has been dispatched by `autocomplete+` to your provider; you should return an array of suggestions (if any) in the order you would like them displayed to the user
* `blacklist` (optional): Defines the scope selector(s) (can be comma-separated) for which your provider should not be used
* `dispose` (optional): Will be called if your provider is being destroyed by `autocomplete+`

```coffeescript
provider =
  selector: '.source.js,.source.coffee' # This provider will be run on JavaScript and Coffee files
  blacklist: '.source.js .comment' # This provider will not be run when the cursor is inside a JavaScript comment
  requestHandler: (options) =>
    # Build your suggestions here...

  dispose: ->
    # Your dispose logic here
```

## Support For Asynchronous Request Handling

Some providers satisfy a suggestion request in an asynchronous way (e.g. it may need to dispatch requests to an external process to get suggestions). To asynchronously provide suggestions, simply return a `Promise` from your `requestHandler`:

```coffeescript
requestHandler: (options) =>
  return new Promise (resolve) =>
    # Build your suggestions here asynchronously...
    resolve(suggestions) # When you are done, call resolve and pass your suggestions to it
```

## Suggestions

Your suggestions should be returned from `requestHandler` as an array of objects with the following properties:

* `word` (required): The text which will be inserted into the editor, in place of the prefix
* `prefix` (required): The text immediately preceding the cursor, which will be replaced by the word (if selected by the user)
* `label` (optional): An indicator (e.g. `function`, `variable`) denoting the "kind" of suggestion this represents
* `renderLabelAsHtml` (optional): If true, indicates that your label includes HTML; if false, your label will be wrapped and styled by `autocomplete+`
* `className` (optional): Allows you to style your suggestion via CSS, if desired
* `onWillConfirm` (optional): If you supply a callback, it will be called _after_ a user has selected a suggestion, but _before_ the suggestion `prefix` is replaced by the suggestion `word` in the buffer
* `onDidConfirm` (optional): If you supply a callback, it will be called _after_ the suggestion `prefix` is replaced by the suggestion `word` in the buffer

```coffeescript
provider =
  selector: '.source.js,.source.coffee' # This provider will be run on JavaScript and Coffee files
  blacklist: '.source.js .comment' # This provider will not be run when the cursor is inside a JavaScript comment
  requestHandler: (options) =>
    [{
      word: 'hello',
      prefix: 'h',
      label: '<span style="color: red">world</span>',
      renderLabelAsHtml: true,
      className: 'globe',
      onWillConfirm: -> # Do something here before the word has replaced the prefix (if you need, you usually don't need to),
      onDidConfirm: -> # Do something here after the word has replaced the prefix (if you need, you usually don't need to)
    }]
  dispose: ->
    # Your dispose logic here
```