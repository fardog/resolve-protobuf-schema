# resolve-protobuf-schema

Read a protobuf schema from the disk, parse it and resolve all imports

```
npm install resolve-protobuf-schema
```

[![build status](http://img.shields.io/travis/fardog/resolve-protobuf-schema.svg?style=flat)](http://travis-ci.org/fardog/resolve-protobuf-schema)

This is a fork of mafintosh's [resolve-protobuf-schema][] which namespaces
imported protobufs if they specify a `package` directive.

## Usage

Store the following example protobuf schema in `test.proto`

```
package com.example.test;

message Test {
  optional string test = 1;
}
```

Then run

``` js
var resolve = require('resolve-protobuf-schema')
console.log(resolve.sync('test.proto')) // prints the parsed schema
```

Schema imports will resolved as well

```
package com.example.anothertest;

import "./test.proto"

message AnotherTest {
  optional string something = 1;
  optional com.example.test.Test test = 2;
}
```

``` js
console.log(resolve.sync('./another-test.proto')) // will print a combined parsed schema
```

## API

* `resolve(path, cb)` read and resolve a schema
* `resolve.sync(path)` sync version of `resolve`

## License

MIT

[resolve-protobuf-schema]: https://github.com/mafintosh/resolve-protobuf-schema
