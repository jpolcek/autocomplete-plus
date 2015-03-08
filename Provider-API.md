The Provider API allows you to make autocomplete+ awesome. The Atom community will ultimately judge the quality of Atom's autocomplete experience by the breadth and depth of the provider ecosystem. We're so excited that you're here reading about how to make Atom awesome.

> The following examples are in CoffeeScript. If you would like to add JavaScript examples, please feel free to edit this page!

## Defining A Provider

```coffee
provider =
  # This will work on JavaScript and CoffeeScript files, but not in js comments.
  selector: '.source.js, .source.coffee'
  disableForSelector: '.source.js .comment'

  # This will take priority over the default provider, which has a priority of 0.
  # `excludeLowerPriority` will suppress any providers with a lower priority
  # i.e. The default provider will be suppressed
  inclusionPriority: 1
  excludeLowerPriority: true

  # Required: Return a promise, an array of suggestions, or null.
  getSuggestions: ({editor, bufferPosition, scopeDescriptor, prefix}) ->
    new Promise (resolve) ->
      resolve([text: 'something'])

  # (optional): called _after_ the suggestion `replacementPrefix` is replaced
  # by the suggestion `text` in the buffer
  onDidInsertSuggestion: ({editor, triggerPosition, suggestion}) ->

  # (optional): called when your provider needs to be cleaned up. Unsubscribe
  # from things, kill any processes, etc.
  dispose: ->
```

The properties of a provider:

* `selector` (required): Defines the scope selector(s) (can be comma-separated) for which your provider should receive suggestion requests
* `getSuggestions` (required): Is called when a suggestion request has been dispatched by `autocomplete+` to your provider. Return an array of suggestions (if any) in the order you would like them displayed to the user. Returning a promise
* `disableForSelector` (optional): Defines the scope selector(s) (can be comma-separated) for which your provider should not be used
* `inclusionPriority` (optional): A number to indicate its priority to be included in a suggestions request. The default provider has an inclusion priority of `0`. Higher priority providers can suppress lower priority providers with `excludeLowerPriority`.
* `excludeLowerPriority` (optional): Will not use lower priority providers when this provider is used.
* `dispose` (optional): Will be called if your provider is being destroyed by `autocomplete+`
* `onDidInsertSuggestion` (optional): Function that is called when a suggestion from your provider was inserted into the buffer
  * `editor`: the [TextEditor](https://atom.io/docs/api/latest/TextEditor) your suggestion was inserted in
  * `triggerPosition`: A [Point](https://atom.io/docs/api/latest/Point) where autocomplete was triggered
  * `suggestion`: The suggestion object that was inserted.

## Support For Asynchronous Request Handling

Some providers satisfy a suggestion request in an asynchronous way (e.g. it may need to dispatch requests to an external process to get suggestions). To asynchronously provide suggestions, simply return a `Promise` from your `getSuggestions`:

```coffeescript
getSuggestions: (options) ->
  return new Promise (resolve) ->
    # Build your suggestions here asynchronously...
    resolve(suggestions) # When you are done, call resolve and pass your suggestions to it
```

## The Suggestion Request's Options Object

An `options` object will be passed to your `getSuggestions` function, with the following properties:

* `editor`: The current `TextEditor`
* `bufferPosition`: The position of the cursor
* `scopeDescriptor`: The [scope descriptor](https://atom.io/docs/latest/advanced/scopes-and-scope-descriptors) for the current cursor position
* `prefix`: The prefix for the word immediately preceding the current cursor position

## Suggestions

```coffee
provider =
  selector: '.source.js, .source.coffee'
  disableForSelector: '.source.js .comment'

  getSuggestions: ({editor, bufferPosition, scopeDescriptor, prefix}) ->
    new Promise (resolve) ->
      # Find your suggestions here
      suggestion =
        text: 'someText' # OR
        snippet: 'someText(${1:myArg})'
        replacementPrefix: 'so' # (optional)
        rightLabel: '' # (optional)
        rightLabelHTML: '' # (optional)
        type: 'function' # (optional)
      resolve([suggestion])
```

Your suggestions should be returned from `getSuggestions` as an array of objects with the following properties:

* `text` (required; or `snippet`): The text which will be inserted into the editor, in place of the prefix
* `snippet` (required; or `text`): A snippet string. This will allow users to tab through function arguments or other options. e.g. `'myFunction(${1:arg1}, ${2:arg2})'`. See the [snippets](https://github.com/atom/snippets) package for more information.
* `replacementPrefix` (optional): The text immediately preceding the cursor, which will be replaced by the `text`. If not provided, the prefix passed into `getSuggestions` will be used.
* `rightLabel` (optional): An indicator (e.g. `function`, `variable`) denoting the "kind" of suggestion this represents
* `rightLabelHTML` (optional): If true, indicates that your label includes HTML; if false, your label will be wrapped and styled by `autocomplete+`
* `className` (optional): Class name for the suggestion in the suggestion list. Allows you to style your suggestion via CSS, if desired

## Registering Your Provider With `autocomplete+`

### API 2.0.0

In your `package.json`, add:

```javascript
"providedServices": {
  "autocomplete.provider": {
    "versions": {
      "2.0.0": "provide"
    }
  }
}
```

Then, in your `main.coffee` (or whatever file you define as your `main` in `package.json` i.e. `"main": "./lib/your-main"` would imply `your-main.coffee`), add the following:

For a single provider:

```coffeescript
provide: ->
  @yourProviderHere
```

For multiple providers, just return an array:

```coffeescript
provide: ->
  [@yourProviderHere, @yourOtherProviderHere]
```

## Provider Examples

We've taken to making each provider its own clean repo:

* [Autocomplete CSS](https://github.com/atom/autocomplete-css)
* [Autocomplete HTML](https://github.com/atom/autocomplete-html)
* [Autocomplete Snippets](https://github.com/atom-community/autocomplete-snippets)

Check out the lib directory in each of these for the code!

## Tips

### Generating a new prefix

The `prefix` passed to `getSuggestions` may not be sufficient for your language. You may need to generate your own prefix. Here is a pattern to use your own prefix:

```coffee
provider =
  selector: '.source.js, .source.coffee'

  getSuggestions: ({editor, bufferPosition}) ->
    prefix = @getPrefix(editor, bufferPosition)

    new Promse (resolve) ->
      suggestion =
        text: 'someText'
        replacementPrefix: prefix
      resolve([suggestion])

  getPrefix: (editor, bufferPosition) ->
    # Whatever your prefix regex might be
    regex = /[\w0-9_-]+$/

    # Get the text for the line up to the triggered buffer position
    line = editor.getTextInRange([[bufferPosition.row, 0], bufferPosition])

    # Match the regex to the line, and return the match
    line.match(regex)?[0] or ''
```
