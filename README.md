angular-cjs
===========

CommonJS module for the browser that exports a reference to AngularJS.

## Problem

As for 1.11.2014 there is only one way to use AngularJS with Browserify without **global angular reference** in your code: using `browserify-shim`.
Still, if you are trying to use packages, which reference angular using CommonJS, shim **will not work** (it works only for app-level bundles).

## Problem example
```javascript```
// my-package/index.js
var angular = require('angular');

module.exports = angular.module('supermodule', [])
  // here some angular-related code
```

If you will now `npm install path/to/my-package` and try to use it like that:
```javascript
// app.js
var myPackage = require('my-package');
```

it will fail during the browserify build with the error "Cannot find module 'angular'" inside `my-package/index.js` even if you have browserify-shim.

## Solution
The only working solution I have found so far is to use `angular-cjs`:
```javascript
/ /my-package/index.js
var angular = require('angular-cjs');

module.exports = angular.module('supermodule', [])
  // here some angular-related code
```