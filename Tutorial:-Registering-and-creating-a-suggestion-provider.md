Since version 0.12.0 other packages can register suggestion providers for autocomplete-plus. Suggestion providers provide words that will be displayed in autocomplete-plus's suggestion list.

Registering a suggestion provider
---------------------------------

Every time a new EditorView is created, we have to register a provider for this specific view. But first, we have to wait for `autocomplete-plus` to load:

```coffeescript
ExampleProvider = require "./example-provider"

module.exports =
  editorSubscription: null
  autocomplete: null
  providers: []
  activate: ->
    atom.packages.activatePackage("autocomplete-plus")
      .then (pkg) =>
        @autocomplete = pkg.mainModule
        @registerProviders()
```

Now, let's register the providers:

```coffeescript
  registerProviders: ->
    @editorSubscription = atom.workspaceView.eachEditorView (editorView) =>
      if editorView.attached and not editorView.mini
        provider = new ExampleProvider editorView

        @autocomplete.registerProviderForEditorView provider, editorView

        @providers.push provider
```

Also, when the package is deactivated, we should clean up:

```coffeescript
  deactivate: ->
    @editorSubscription?.off()
    @editorSubscription = null

    @providers.forEach (provider) =>
      @autocomplete.unregisterProvider provider

    @providers = []
```

That's it for now. Let's implement the provider!

Implementing the provider
-------------------------

A suggestion provider is a class that inherits from autocomplete-plus's [Provider](https://github.com/saschagehlich/autocomplete-plus/blob/master/lib/provider.coffee) class:

```coffeescript
{Provider, Suggestion} = require "autocomplete-plus"
class ExampleProvider extends Provider
```

As you see, we also grab the [Suggestion](https://github.com/saschagehlich/autocomplete-plus/blob/master/lib/suggestion.coffee) class from autocomplete-plus. We will need this in the next step. 

Now, this provider does nothing. Actually, you will run into error messages, since this provider does not override the `buildSuggestions()` method. Let's implement it:

```coffeescript
  buildSuggestions: ->
    suggestions = []
    suggestions.push new Suggestion(this, word: "async", label: "@async")
    suggestions.push new Suggestion(this, word: "attribute", label: "@attribute")
    suggestions.push new Suggestion(this, word: "author", label: "@author")
    suggestions.push new Suggestion(this, word: "beta", label: "@beta")
    suggestions.push new Suggestion(this, word: "borrows", label: "@borrows")
    suggestions.push new Suggestion(this, word: "bubbles", label: "@bubbles")
    return suggestions
```

And voilà, this is the result:

![ExampleProvider](http://s7.directupload.net/images/140411/vcokpfiv.png)

Content-aware suggestions
-------------------------

Our example provider always displays the same suggestions, even though we typed something that has nothing to do with the suggestions. So let's make the suggestions content-aware, meaning that we only want to display our suggestions when we have typed `@`, followed by a word.

`Provider` also provides a couple of helper methods. One of them is `#prefixOfSelection(Selection)` that gives us the last match of `@wordRegex` before `Selection`. Let's set the `@wordRegex`, grab the current selection (in this case it's just the cursor position) and find the last match:

```coffeescript
  wordRegex: /@\b\w*[a-zA-Z_]\w*\b/g
  buildSuggestions: ->
    selection = @editor.getSelection()
    prefix = @prefixOfSelection selection
    return unless prefix.length

    suggestions = []
    suggestions.push new Suggestion(this, word: "async", label: "@async")
    suggestions.push new Suggestion(this, word: "attributes", label: "@attribute")
    suggestions.push new Suggestion(this, word: "author", label: "@author")
    suggestions.push new Suggestion(this, word: "beta", label: "@beta")
    suggestions.push new Suggestion(this, word: "borrows", label: "@borrows")
    suggestions.push new Suggestion(this, word: "bubbles", label: "@bubbles")
    return suggestions
```

Now we only see the suggestions when entering a string that starts with `@`:

![ExampleProvider](http://s1.directupload.net/images/140411/4kbtec9e.png)

But we still see _all_ suggestions. Let's filter them! We're using the `fuzzaldrin` package to do fuzzy string matching.

```coffeescript
{Provider, Suggestion} = require "autocomplete-plus"
fuzzaldrin = require "fuzzaldrin"
class ExampleProvider extends Provider
  wordRegex: /@\b\w*[a-zA-Z_]\w*\b/g
  possibleWords: ["async", "attributes", "author", "beta", "borrows", "bubbles"]
  buildSuggestions: ->
    selection = @editor.getSelection()
    prefix = @prefixOfSelection selection
    return unless prefix.length

    suggestions = @findSuggestionsForPrefix prefix
    return unless suggestions.length
    return suggestions

  findSuggestionsForPrefix: (prefix) ->
    # Get rid of the leading @
    prefix = prefix.replace /^@/, ''

    # Filter the words using fuzzaldrin
    words = fuzzaldrin.filter @possibleWords, prefix

    # Builds suggestions for the words
    suggestions = for word in words when word isnt prefix
      new Suggestion this, word: word, prefix: prefix, label: "@#{word}"

    return suggestions
```

The result:

![ExampleProvider](http://s7.directupload.net/images/140411/56k2sne7.gif)

Custom confirmation actions
---------------------------

Per default, when the user confirms the autocompletion, `autocomplete-plus` will just replace the Suggestion's `prefix` attribute with the given `word`. Let's replace it with some custom content by overriding the `confirm(Suggestion)` method.

As the return value, `confirm` expects a Boolean. If it returns `true`, it will use the default behavior. If it returns a falsy value, it won't.

Our `possibleWords` array will now look like this:

```coffeescript
  possibleWords: [
    { word: "async", label: "@async", body: "@async" },
    { word: "attribute", label: "@attribute", body: "@attribute [name]" },
    { word: "beta", label: "@beta", body: "@beta" },
    { word: "borrows", label: "@borrows", body: "@borrows [otherMemberName] as [thisMemberName]" },
    { word: "bubbles", label: "@bubbles", body: "@bubbles [name]" }
  ]
```

Let's override `confirm(Suggestion)`:

```coffeescript
  confirm: (suggestion) ->
    selection = @editor.getSelection()
    startPosition = selection.getBufferRange().start
    buffer = @editor.getBuffer()

    # Replace the prefix with the body
    cursorPosition = @editor.getCursorBufferPosition()
    buffer.delete Range.fromPointWithDelta(cursorPosition, 0, -suggestion.prefix.length)
    @editor.insertText suggestion.data.body

    # Move the cursor behind the body
    suffixLength = suggestion.data.body.length - suggestion.prefix.length
    @editor.setSelectedBufferRange [startPosition, [startPosition.row, startPosition.column + suffixLength]]

    return false # Don't fall back to the default behavior
```

And let's update our `findSuggestionsForPrefix` method as well:

```coffeescript
  findSuggestionsForPrefix: (prefix) ->
    # Get rid of the leading @
    prefix = prefix.replace /^@/, ''

    wordsByWord = {}
    words = for word in @possibleWords
      wordsByWord[word.word] = word
      word.word

    # Filter the words using fuzzaldrin
    results = fuzzaldrin.filter words, prefix

    # Builds suggestions for the words
    suggestions = for result in results when word isnt prefix
      word = wordsByWord[result]
      new Suggestion this,
        word: word.word
        prefix: "@#{prefix}"
        label: word.label
        data:
          body: word.body

    return suggestions
```

Et voilà! We're done:

![ExampleProvider](http://s7.directupload.net/images/140411/qoxz2k7h.gif)