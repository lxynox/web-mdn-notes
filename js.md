
# JavaScript

## Module System

**Create custom modules**

skeleton code:

```javascript
'use strict'

(function defineMyModule (global, factory) {
  if (typeof exports === 'object' && exports && typeof exports.nodeName !== 'string') {
    factory(exports); // CommonJS
  } else if (typeof define === 'function' && define.amd) {
    define(['exports'], factory); // AMD
  } else {
    global.MyModule = {};
    factory(global.MyModule); // script, wsh, asp
  }
}(this, function mustacheFactory (MyModule) {

    // custom code

    // local `vars`, `functions`
    // ...
    // utilities, classes, api functions

    // public api
    /*
        MyModule.api1 = ...
        MyModule.api2 = ...
        ...
    */
}))
```

or

```javascript
(function(define) {
    // Global namespace:
    //     var myModule = xxx
    //
    // ## Config
    // ...
    // ## Utilities
    // ...
    // ## Preparation
    // ...
    // ## API
    define('MyModule', function(require, exports, module) {
        module.exports = myModule
    })

}(typeof define === 'function' && define.amd? define : function(id, factory) {
    // Define it the AMD way
    if (typeof exports !== 'undefined') {
        factory(require, exports, module)
    } else {
        var mod = {};
        var exp = {};

        factory(function (value) {
            return window[value];
        }, exp, mod);

        if (mod.exports) {
            // Defining output using `module.exports`
            window[id] = mod.exports;
        } else {
            // Defining output using `exports.*`
            window[id] = exp;
        }
    }
}))
```
