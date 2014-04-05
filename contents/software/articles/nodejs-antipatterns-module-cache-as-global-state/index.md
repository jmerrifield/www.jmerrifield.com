---
title: "Node.js Antipatterns: Module Cache as Global State"
date: 2014-04-07 12:00
template: article.jade
---

I want to share something I've been considering an anti-pattern, involving Node's module cache. Specifically, initializing a module in one part of the program, knowing that subsequent `require` calls will return the already-initialized module.

Node caches modules internally, which makes this sort of thing possible:

```javascript
// index.js (entry point of app)

var redisConnection = /* Redis initialization */

require('./session-store').init({
  connection: redisConnection
})

require('./some-other-module')
```

```javascript
// some-other-module.js

var sessions = require('./session-store')

// sessions is already configured thanks to the .init call in index.js
sessions.get(sessionId, function (err, data) {
  console.log('Session data:', data)
})
```

In `some-other-module` we are assured that `sessions` is the same instance of `./session-store` that we initialized in `index.js`. This gives us an opportunity to pre-configure a module in your program's entry point, and other parts of the program can easily grab a configured instance of that module.

Don't be fooled, this is not a good idea!

Firstly, Node [does not guarantee this behavior](http://nodejs.org/api/modules.html#modules_module_caching_caveats) in all situations. Personally I've never seen two `require` calls return different instances of a module, but that's most likely down to my usage patterns. In particular, on my current project we're supplying a custom `NODE_PATH` so that all `require` paths are relative to the project root.

More significantly, **this is just global state**. All the well-worn advice about the evils of global variables applies here. Any part of the system can change this state. Relying on one part of the system to set global state *before* another part of the system tries to use it, makes the system very hard to reason about and debug, and tends to make code reuse a lot harder. If you suddenly need a second instance of that module (e.g. a secondary session store talking to a different database) then a large amount of re-work would be needed.

It's not always 'bad' to do this. It's reasonable to memoize expensive lookups inside a module, and in that case you can encapsulate the cache data and make the lookup transparent, so that the consumer neither needs to know, nor can it interfere with, the sequence of operations.

```javascript
var cachedData

module.exports.getData = function (callback) {
  if (cachedData) {
    return process.nextTick(function () { callback(cachedData) })
  }

  require('expensiveDataSource').fetchData(function (data) {
    cachedData = data; callback(data)
  })
}
```

Generally though, if a module is stateful, it's better to have it return a new instance of an object (or function) that contains the state and provides the interface to manipulate it. Make it the responsibility of the consumer to keep track of configured instances. It's also helpful to provide a narrow interface that makes it difficult to inadvertently try and use an invalid instance.

```javascript
var config

module.exports.init = function (c) {
  config = c
}

module.exports.doStuff = function () {
  return doThingsWith(config)
}
```

Becomes:

```javascript
module.exports.init = function (config) {
  if (!configOk(config)) {
    throw new Error('this config will result in a broken instance!')
  }

  return {
    doStuff: function () {
      return doThingsWith(config)
    }
  }
}
```

Now, we have a fairly strong guarantee that nobody will be able to call `doStuff` without having first configured the module with valid settings (in the first example, this would have been easy to do inadvertently). In addition, we're free to use multiple instances of this module with different configurations if that becomes useful.

Sadly this makes it more difficult for 'far-away' parts of the program to make use of pre-configured modules. Passing them around through a long dependency chain can get very verbose and hard to keep track of. IoC containers are very popular in the Java and .NET world for dealing with this, but they are not so common in the Node community ([wire](https://github.com/cujojs/wire) seems to be the main contender at the time of writing). Whether you investigate an IoC tool, or find some other acceptable way of passing around configured module instances, it's worth the effort to remove this avenue of complexity.
