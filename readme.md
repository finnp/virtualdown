# virtualdown
Windows | Mac/Linux
------- | ---------
[![Windows Build status](http://img.shields.io/appveyor/ci/finnp/virtualdown.svg)](https://ci.appveyor.com/project/finnp/virtualdown/branch/master) | [![Build Status](https://travis-ci.org/finnp/virtualdown.svg?branch=master)](https://travis-ci.org/finnp/virtualdown) 

Wraps a leveldown-compatible module as such as no changes are made on the original
database instance. Instead it writes all `put/del` to memory. When performing `get`
it first checks the memory and only fetched from the original source if it's not 
in memory. This means when using `virtualdown` it looks like the original database
is changed, but in reality nothing is.

Install with `npm install virtualdown`

You can get your leveldown drop-in by wrapping it around another leveldown module:
```js
var myVirtualDown = require('virtualdown')(somethingDOWN)
```

It is a generalisation of the [virtual-leveldown](https://www.npmjs.org/package/virtual-leveldown) module.

## example

```js
var virtualDown = require('virtualdown')
var leveldown = require('leveldown')

var virtualLevelDown = virtualDOWN(leveldown)

var db = virtualLevelDown('mydatabase') // filled with cats

db.open(function () {
    db.put('doggy', 'dogdog', function (err) {
      db.get('doggy', function (value) {
        // value == 'dogdog'
        // but the dog is not in 'mydatabase' on disk
      })
    })
})
```