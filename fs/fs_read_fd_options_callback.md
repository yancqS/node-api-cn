<!-- YAML
added: v13.11.0
changes:
  - version: v13.11.0
    pr-url: https://github.com/nodejs/node/pull/31402
    description: Options object can be passed in
                 to make Buffer, offset, length and position optional
-->
* `fd` {integer}
* `options` {Object}
  * `buffer` {Buffer|TypedArray|DataView} **默认值:** `Buffer.alloc(16384)`
  * `offset` {integer} **默认值:** `0`
  * `length` {integer} **默认值:** `buffer.length`
  * `position` {integer} **默认值:** `null`
* `callback` {Function}
  * `err` {Error}
  * `bytesRead` {integer}
  * `buffer` {Buffer}

与上述fs.read函数类似，此版本带有一个可选的options对象。 如果未指定options对象，则使用使用上述默认值。

