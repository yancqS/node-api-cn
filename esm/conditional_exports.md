
Conditional exports provide a way to map to different paths depending on
certain conditions. They are supported for both CommonJS and ES module imports.

For example, a package that wants to provide different ES module exports for
`require()` and `import` can be written:

<!-- eslint-skip -->
```js
// package.json
{
  "main": "./main-require.cjs",
  "exports": {
    "import": "./main-module.js",
    "require": "./main-require.cjs"
  },
  "type": "module"
}
```

Node.js supports the following conditions:

* `"import"` - matched when the package is loaded via `import` or
   `import()`. Can reference either an ES module or CommonJS file, as both
   `import` and `import()` can load either ES module or CommonJS sources.
* `"require"` - matched when the package is loaded via `require()`.
   As `require()` only supports CommonJS, the referenced file must be CommonJS.
* `"node"` - matched for any Node.js environment. Can be a CommonJS or ES
   module file. _This condition should always come after `"import"` or
   `"require"`._
* `"default"` - the generic fallback that will always match. Can be a CommonJS
   or ES module file. _This condition should always come last._

Condition matching is applied in object order from first to last within the
`"exports"` object. _The general rule is that conditions should be used
from most specific to least specific in object order._

Other conditions such as `"browser"`, `"electron"`, `"deno"`, `"react-native"`,
etc. are ignored by Node.js but may be used by other runtimes or tools.
Further restrictions, definitions or guidance on condition names may be
provided in the future.

Using the `"import"` and `"require"` conditions can lead to some hazards,
which are explained further in
[the dual CommonJS/ES module packages section][].

Conditional exports can also be extended to exports subpaths, for example:

<!-- eslint-skip -->
```js
{
  "main": "./main.js",
  "exports": {
    ".": "./main.js",
    "./feature": {
      "browser": "./feature-browser.js",
      "default": "./feature.js"
    }
  }
}
```

Defines a package where `require('pkg/feature')` and `import 'pkg/feature'`
could provide different implementations between the browser and Node.js,
given third-party tool support for a `"browser"` condition.

