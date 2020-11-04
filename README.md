# cppzst

![Test Status](https://github.com/scheibo/z-std/workflows/Tests/badge.svg)
![License](https://img.shields.io/badge/License-MIT-blue.svg)
[![npm version](https://img.shields.io/npm/v/scheibo/z-std.svg)](https://www.npmjs.com/package/scheibo/z-std)

Zstandard wrapper for Node with Typescript bindings.

## Installation

```bash
$ npm install z-std --save
```

## Usage

### Async

#### `compress(buffer[, zstdCompressParams], callback)`

```js
import {compress} from 'cppzst';

await compress(input);

```

#### `decompress(buffer[, zstdDecompressParams], callback)`

```js
import {decompress} from 'cppzst';

await decompress(input);
```

### Sync

#### `compressSync(buffer[, zstdCompressParams])`

```js
const compressSync = require('cppzst').compressSync;

try {
  const output = compressSync(input);
} catch(err) {
  // ...
}
```

#### `decompressSync(buffer[, zstdCompressParams])`

```js
const decompressSync = require('cppzst').decompressSync;

try {
  const output = decompressSync(input);
} catch(err) {
  // ...
}
```

### Stream

#### `compressStream([zstdCompressParams])`

```js
const compressStream = require('cppzst').compressStream;
const fs = require('fs');

fs.createReadStream('path/to/input')
  .pipe(compressStream())
  .pipe(fs.createWriteStream('path/to/output'));
```

#### `decompressStream([zstdCompressParams])`

```js
const decompressStream = require('cppzst').decompressStream;
const fs = require('fs');

fs.createReadStream('path/to/input')
  .pipe(decompressStream())
  .pipe(fs.createWriteStream('path/to/output'));
```

### ZSTD Params

The `compress`, `compressSync` and `compressStream` methods may accept an optional
`zstdCompressParams` object to define compress level and/or dict.

```js
const zstdCompressParams = {
  level: 5, // default 1
  dict: new Buffer('hello zstd'), // if dict null, left level only.
  dictSize: dict.length  // if dict null, left level only.
};
```

The `decompress`, `decompressSync` and `decompressStream` methods may accept an optional
`zstdDecompressParams` object to define dict.

```js
const zdtdDecompressParams = {
  dict: new Buffer('hello zstd'),
  dictSize: dict.length,
};
```

## Tests

```sh
$ npm test
```

## License

This package is distributed under the terms of the [MIT License](LICENSE).
