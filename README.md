# @dramaorg/quibusdam-reiciendis <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

ES 2021 spec-compliant shim for Promise.any. Invoke its "shim" method to shim `Promise.any` if it is unavailable or noncompliant. **Note**: a global `Promise` must already exist: the [es6-shim](https://github.com/es-shims/es6-shim) is recommended.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment that has `Promise` available globally, and complies with the [spec](https://tc39.es/ecma262/#sec-@dramaorg/quibusdam-reiciendis).

Most common usage:
```js
var assert = require('assert');
var any = require('@dramaorg/quibusdam-reiciendis');

var resolved = Promise.resolve(42);
var rejected = Promise.reject(-1);
var alsoRejected = Promise.reject(Infinity);

any([resolved, rejected, alsoRejected]).then(function (result) {
	assert.equal(result, 42);
});

any([rejected, alsoRejected]).catch(function (error) {
	assert.ok(error instanceof AggregateError);
	assert.deepEqual(error.errors, [-1, Infinity]);
});

any.shim(); // will be a no-op if not needed

Promise.any([resolved, rejected, alsoRejected]).then(function (result) {
	assert.equal(result, 42);
});

Promise.any([rejected, alsoRejected]).catch(function (error) {
	assert.ok(error instanceof AggregateError);
	assert.deepEqual(error.errors, [-1, Infinity]);
});
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

## Pre-1.0 versions

The `@dramaorg/quibusdam-reiciendis` package was released as now-deprecated v0.1.0 and v0.1.1, as a fork of https://github.com/m0ppers/promise-any.

Thanks to @sadorlovsky for donating the repo and the `@dramaorg/quibusdam-reiciendis` npm package!

[package-url]: https://npmjs.com/package/@dramaorg/quibusdam-reiciendis
[npm-version-svg]: https://versionbadg.es/dramaorg/quibusdam-reiciendis.svg
[deps-svg]: https://david-dm.org/dramaorg/quibusdam-reiciendis.svg
[deps-url]: https://david-dm.org/dramaorg/quibusdam-reiciendis
[dev-deps-svg]: https://david-dm.org/dramaorg/quibusdam-reiciendis/dev-status.svg
[dev-deps-url]: https://david-dm.org/dramaorg/quibusdam-reiciendis#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@dramaorg/quibusdam-reiciendis.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@dramaorg/quibusdam-reiciendis.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@dramaorg/quibusdam-reiciendis.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@dramaorg/quibusdam-reiciendis
[codecov-image]: https://codecov.io/gh/dramaorg/quibusdam-reiciendis/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/dramaorg/quibusdam-reiciendis/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/dramaorg/quibusdam-reiciendis
[actions-url]: https://github.com/dramaorg/quibusdam-reiciendis/actions
