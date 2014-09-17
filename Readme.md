# metalsmith-each

A [Metalsmith](https://github.com/segmentio/metalsmith) plugin that allows you apply a function to each file or filename.


## Installation

    $ npm install metalsmith-each

## Usage

Just pass a function to metalsmith-each that accepts the metalsmith file object
and, optionally, the filename.

```js
var each = require('metalsmith-each');

metalsmith.use(
  each(function (file, filename) {
    file.date = new Date();
  }
));

```

To change the filename, just return a string with the new name.

```js
var each = require('metalsmith-each');

metalsmith.use(
  each(function (file, filename) {
    return filename.toUpperCase();
  }
));
```

Functions can be async, too. Just accept a `done()` function as the third
argument.  Note: If you accept the done function, you must call it or your build
will hang.

```js
var each = require('metalsmith-each');

metalsmith.use(
  each(function (file, filename, done) {
    setTimeout(function () {
      file.date = new Date();
      done();
    }, 1000);
  }
));
```

To rename a file with an async function, pass the new name to the `done()`
function.

```js
var each = require('metalsmith-each');

metalsmith.use(
  each(function (file, filename, done) {
    setTimeout(function () {
      done(filename.toUpperCase());
    }, 1000);
  }
));
```


## License

  MIT
