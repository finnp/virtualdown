# virtualdown

LevelDOWN drop-in replacement that reads from a leveldown store, but writes
to memory. It behaves like any leveldown, but all changes (put / del) are only made
in memory, so that the original leveldown instance remains unchanged.

Install with `npm install virtualdown`

## example

```js
var virtualDOWN = require('virtual-leveldown')

var db = virtualDOWN('mydatabase') // filled with cats

db.open(function () {
    db.put('doggy', 'dogdog', function (err) {
      db.get('doggy', function (value) {
        // value == 'dogdog'
        // but the dog is not in 'mydatabase' on disk
      })
    })
})
```