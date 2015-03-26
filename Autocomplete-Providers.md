## Built-In Providers

| Grammar | Selector | Provider         | Status                               |
|:--------|:---------|:-----------------|:-------------------------------------|
| All     | `*`      | `FuzzyProvider`  | `Deprecated`                         |
| All     | `*`      | `SymbolProvider` | `WIP` (Will Replace `FuzzyProvider`) |

## Providers For Built-In Grammars

| Grammar                                                                          | Selector                             | Provider                                                            | API Status |
|:---------------------------------------------------------------------------------|:-------------------------------------|:--------------------------------------------------------------------|:-----------|
| Null Grammar                                                                     | `.text.plain.null-grammar`           | &nbsp;                                                              | &nbsp;     |
| [CoffeeScript (Literate)](https://atom.io/packages/language-coffee-script)       | `.source.litcoffee`                  |                                                                     |            |
| [CoffeeScript](https://atom.io/packages/language-coffee-script)                  | `.source.coffee`                     |                                                                     |            |
| [JSON](https://atom.io/packages/language-json)                                   | `.source.json`                       |                                                                     |            |
| [Shell Session](https://atom.io/packages/language-shellscript)                   | `.text.shell-session`                |                                                                     |            |
| [Shell Script](https://atom.io/packages/language-shellscript)                    | `.source.shell`                      |                                                                     |            |
| [Hyperlink](https://atom.io/packages/language-hyperlink)                         | `.text.hyperlink`                    |                                                                     |            |
| [TODO](https://atom.io/packages/language-todo)                                   | `.text.todo`                         |                                                                     |            |
| [C](https://atom.io/packages/language-c)                                         | `.source.c`                          |                                                                     |            |
| [C++](https://atom.io/packages/language-c)                                       | `.source.cpp`                        | [atom-hack](https://atom.io/packages/atom-hack)                     | `1.0.0`    |
| [Clojure](https://atom.io/packages/language-clojure)                             | `.source.clojure`                    |                                                                     |            |
| [CSS](https://atom.io/packages/language-css)                                     | `.source.css`                        | [autocomplete-css](https://atom.io/packages/autocomplete-css)       | `2.0.0`    |
| [GitHub Markdown](https://atom.io/packages/language-gfm)                         | `.source.gfm`                        | [autocomplete-bibtex](https://atom.io/packages/autocomplete-bibtex) | `1.1.0`    |
| [Git Config](https://atom.io/packages/language-git)                              | `.source.git-config`                 |                                                                     |            |
| [Git Commit Message](https://atom.io/packages/language-git)                      | `.text.git-commit`                   |                                                                     |            |
| [Git Rebase Message](https://atom.io/packages/language-git)                      | `.text.git-rebase`                   |                                                                     |            |
| [HTML (Go)](https://atom.io/packages/language-go)                                | `.text.html.gohtml`                  |                                                                     |            |
| [Go](https://atom.io/packages/language-go)                                       | `.source.go`                         | [go-plus](https://atom.io/packages/go-plus)                         | `2.0.0`    |
| [Go Template](https://atom.io/packages/language-go)                              | `.source.gotemplate`                 |                                                                     |            |
| [HTML](https://atom.io/packages/language-html)                                   | `.text.html.basic`                   | [autocomplete-html](https://atom.io/packages/autocomplete-html)     | `2.0.0`    |
| [JavaScript](https://atom.io/packages/language-javascript)                       | `.source.js`                         | [atom-ternjs](https://atom.io/packages/atom-ternjs)                 | `2.0.0`    |
| [Java Properties](https://atom.io/packages/language-java)                        | `.source.java-properties`            |                                                                     |            |
| [Regular Expressions (JavaScript)](https://atom.io/packages/language-javascript) | `.source.js.regexp`                  |                                                                     |            |
| [JavaServer Pages](https://atom.io/packages/language-java)                       | `.text.html.jsp`                     |                                                                     |            |
| [Java](https://atom.io/packages/language-java)                                   | `.source.java`                       |                                                                     |            |
| [JUnit Test Report](https://atom.io/packages/language-java)                      | `.text.junit-test-report`            |                                                                     |            |
| [Makefile](https://atom.io/packages/language-make)                               | `.source.makefile`                   |                                                                     |            |
| [LESS](https://atom.io/packages/language-less)                                   | `.source.css.less`                   |                                                                     |            |
| [SQL (Mustache)](https://atom.io/packages/language-mustache)                     | `.source.sql.mustache`               |                                                                     |            |
| [HTML (Mustache)](https://atom.io/packages/language-mustache)                    | `.text.html.mustache`                |                                                                     |            |
| [Objective-C++](https://atom.io/packages/language-objective-c)                   | `.source.objcpp`                     |                                                                     |            |
| [Strings File](https://atom.io/packages/language-objective-c)                    | `.source.strings`                    |                                                                     |            |
| [Objective-C](https://atom.io/packages/language-objective-c)                     | `.source.objc`                       |                                                                     |            |
| [Property List (XML)](https://atom.io/packages/language-property-list)           | `.text.xml.plist`                    |                                                                     |            |
| [Property List (Old-Style)](https://atom.io/packages/language-property-list)     | `.source.plist`                      |                                                                     |            |
| [Perl](https://atom.io/packages/language-perl)                                   | `.source.perl`                       |                                                                     |            |
| [PHP](https://atom.io/packages/language-php)                                     | `.text.html.php`                     |                                                                     |            |
| PHP                                                                              | `.source.php`                        | [atom-hack](https://atom.io/packages/atom-hack)                     | `1.1.0`    |
| [Python Console](https://atom.io/packages/language-python)                       | `.text.python.console`               |                                                                     |            |
| [Python Traceback](https://atom.io/packages/language-python)                     | `.text.python.traceback`             |                                                                     |            |
| [Regular Expressions (Python)](https://atom.io/packages/language-python)         | `.source.regexp.python`              |                                                                     |            |
| [Python](https://atom.io/packages/language-python)                               | `.source.python`                     |                                                                     |            |
| [Ruby on Rails (RJS)](https://atom.io/packages/language-ruby-on-rails)           | `.source.ruby.rails.rjs`             |                                                                     |            |
| [Ruby](https://atom.io/packages/language-ruby)                                   | `.source.ruby`                       |                                                                     |            |
| [HTML (Ruby - ERB)](https://atom.io/packages/language-ruby)                      | `.text.html.erb`                     |                                                                     |            |
| [HTML (Rails)](https://atom.io/packages/language-ruby-on-rails)                  | `.text.html.ruby`                    |                                                                     |            |
| [SQL (Rails)](https://atom.io/packages/language-ruby-on-rails)                   | `.source.sql.ruby`                   |                                                                     |            |
| [JavaScript (Rails)](https://atom.io/packages/language-ruby-on-rails)            | `.source.js.rails .source.js.jquery` |                                                                     |            |
| [Ruby on Rails](https://atom.io/packages/language-ruby-on-rails)                 | `.source.ruby.rails`                 |                                                                     |            |
| [Sass](https://atom.io/packages/language-sass)                                   | `.source.sass`                       |                                                                     |            |
| [Plain Text](https://atom.io/packages/language-text)                             | `.text.plain`                        |                                                                     |            |
| [SCSS](https://atom.io/packages/language-sass)                                   | `.source.css.scss`                   |                                                                     |            |
| [SQL](https://atom.io/packages/language-sql)                                     | `.source.sql`                        |                                                                     |            |
| [TOML](https://atom.io/packages/language-toml)                                   | `.source.toml`                       |                                                                     |            |
| [XSL](https://atom.io/packages/language-xml)                                     | `.text.xml.xsl`                      |                                                                     |            |
| [XML](https://atom.io/packages/language-xml)                                     | `.text.xml`                          |                                                                     |            |
| [YAML](https://atom.io/packages/language-yaml)                                   | `.source.yaml`                       |                                                                     |            |

## Providers For Third-Party Grammars

| Grammar                                                    | Selector           | Provider                                                                | API Status            |
|:-----------------------------------------------------------|:-------------------|:------------------------------------------------------------------------|:----------------------|
| [Apex](https://atom.io/packages/mavensmate-atom)           | `.source.apex`     | [mavensmate-atom](https://atom.io/packages/mavensmate-atom)             | `1.0.0`               |
| [AsciiDoc](https://atom.io/packages/language-asciidoc)     | `.source.asciidoc` | [asciidoc-preview](https://atom.io/packages/asciidoc-preview)           | `Uses Deprecated API` |
| [C#](https://atom.io/packages/language-csharp)             | `.source.cs`       | [omnisharp-atom](https://atom.io/packages/omnisharp-atom)               | `1.0.0`               |
| [Elixir](https://atom.io/packages/language-elixir)         | `.source.elixir`   | [autocomplete-elixir](https://atom.io/packages/autocomplete-elixir)               | `0.1.0`               |
| [Erlang](https://atom.io/packages/language-erlang)         | `.source.erlang`   | [autocomplete-erlang](https://atom.io/packages/autocomplete-erlang)               | `0.1.3`               |
| [GLSL](https://atom.io/packages/language-glsl)             | `.source.glsl`     | [autocomplete-glsl](https://atom.io/packages/autocomplete-glsl)         | `2.0.0`               |
| [Haskell](https://atom.io/packages/language-haskell)       | `.source.haskell`  | [autocomplete-haskell](https://atom.io/packages/autocomplete-haskell)   | `1.0.0`               |
| [Haskell](https://atom.io/packages/language-haskell)       | `.source.haskell`  | [ide-haskell](https://atom.io/packages/ide-haskell)                     | `1.0.0`               |
| [Haxe](https://atom.io/packages/language-haxe)             | `.source.haxe`     | [autocomplete-haxe](https://atom.io/packages/autocomplete-haxe)         | `1.1.0`               |
| [Rust](https://atom.io/packages/language-rust)             | `.source.rust`     | [racer](https://atom.io/packages/racer)                                 | `1.0.0`               |
| [Typescript](https://atom.io/packages/atom-typescript)     | `.source.ts`       | [atom-typescript](https://atom.io/packages/atom-typescript)             | `2.0.0`               |
| [Typescript](https://atom.io/packages/language-typescript) | `.source.ts`       | [atom-typescript-tools](https://atom.io/packages/atom-typescript-tools) | `1.0.0`               |
| [Visualforce](https://atom.io/packages/mavensmate-atom)    | `.visualforce`     | [mavensmate-atom](https://atom.io/packages/mavensmate-atom)             | `1.1.0`               |

## Providers Not Tied To A Specific Grammar

| Selector                                                                                | Provider                                                                  | Status  |
|:----------------------------------------------------------------------------------------|:--------------------------------------------------------------------------|:--------|
| `*`                                                                                     | [autocomplete-emojis](https://atom.io/packages/autocomplete-emojis)       | `1.0.0` |
| `*`                                                                                     | [autocomplete-snippets](https://atom.io/packages/autocomplete-snippets)   | `2.0.0` |
| `*`                                                                                     | [autocomplete-paths](https://atom.io/packages/autocomplete-paths)         | `1.0.0` |
| `*`                                                                                     | [atom-ctags](https://atom.io/packages/atom-ctags)                         | `1.0.0` |
| `.source.js, .source.jsx`                                                               | [ide-flow](https://atom.io/packages/ide-flow)                             | `1.1.0` |
| `.source.css`, `.source.css.less`, `.source.sass`, `.source.css.scss`, `.source.stylus` | [project-palette-finder](https://atom.io/packages/project-palette-finder) | `1.1.0` |
| `*`                                                                                     | [you-complete-me](https://atom.io/packages/you-complete-me)               | `2.0.0` |

--

## Providers Requested By The Community

If you'd like to contribute and are interested in learning how to write an `autocomplete-plus` [`Provider`](https://github.com/atom-community/autocomplete-plus/wiki/Provider-API), start here:

* Emmet: https://github.com/atom-community/autocomplete-plus/issues/156
* LESS: https://github.com/atom-community/autocomplete-plus/issues/151

## Packages That Claim Autocomplete, But Are Not API 1.0.0 Compatible

* https://github.com/Peekmo/atom-autocomplete-php (never published, unknown state)
* https://github.com/kbrownlees/autocomplete-python-jedi (never published, unknown state)
* https://github.com/maun/atom-rust-plus (never published, uses [autocomplete-plus-async](https://atom.io/packages/autocomplete-plus-async))
* https://atom.io/packages/ios (doesn't make use of autocomplete-plus)
* https://atom.io/packages/language-hn (see: https://github.com/ignaciocases/language-hn/issues/1 for API 1.0.0 compatibility)
* https://atom.io/packages/rsense (see: https://github.com/rsense/atom-rsense/issues/1 for API 1.0.0 compatibility)

## Deprecated Providers

If you are using one of these providers, please uninstall the package as it is no longer maintained.

* https://github.com/vito/atom-autocomplete-gocode (deprecated, use [go-plus](https://atom.io/packages/go-plus) instead)

## Other Forks Of Autocomplete

* https://atom.io/packages/autocomplete-clang (fork of `autocomplete`)
* https://github.com/xumingthepoet/autocomplete-plus-elixir (never published)
* https://atom.io/packages/autocomplete-jedi (fork of `autocomplete`)
* https://atom.io/packages/rubymotion (extends default autocomplete package)