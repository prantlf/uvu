<div align="center">
  <img src="shots/uvu.jpg" alt="uvu" height="120" />
</div>

<div align="center">
  <a href="https://npmjs.org/package/uvu">
    <img src="https://badgen.now.sh/npm/v/uvu" alt="version" />
  </a>
  <a href="https://github.com/lukeed/uvu/actions">
    <img src="https://github.com/lukeed/uvu/workflows/CI/badge.svg" alt="CI" />
  </a>
  <a href="https://npmjs.org/package/uvu">
    <img src="https://badgen.now.sh/npm/dm/uvu" alt="downloads" />
  </a>
  <a href="https://packagephobia.now.sh/result?p=uvu">
    <img src="https://packagephobia.now.sh/badge?p=uvu" alt="install size" />
  </a>
</div>

<div align="center">
  <b>uvu</b> is an extremely fast and lightweight test runner for Node.js and the browser<br>
  <b>U</b>ltimate <b>V</b>elocity, <b>U</b>nleashed<br><br>
  <img width="380" alt="example with suites" src="shots/suites.gif"/>
</div>


## Features

* Super [lightweight](https://npm.anvaka.com/#/view/2d/uvu)
* Extremely [performant](#benchmarks)
* Individually executable test files
* Supports `async`/`await` tests
* Supports native ES Modules
* Browser-Compatible
* Familiar API

This fork includes benchmarks with up-to-date versions of test frameworks and additional ones - `baretest`, `jasmine`, `pta`, `tap`, `test` and `zora` - including sizes of their NPM packages, all executed in the current Node.js 14 LTS. See the [benchmark results](#benchmarks) below.

## Install

```
$ npm install --save-dev uvu
```


## Usage

> Check out [`/examples`](/examples) for a list of working demos!

```js
// tests/demo.js
import { test } from 'uvu';
import * as assert from 'uvu/assert';

test('Math.sqrt()', () => {
  assert.is(Math.sqrt(4), 2);
  assert.is(Math.sqrt(144), 12);
  assert.is(Math.sqrt(2), Math.SQRT2);
});

test('JSON', () => {
  const input = {
    foo: 'hello',
    bar: 'world'
  };

  const output = JSON.stringify(input);

  assert.snapshot(output, `{"foo":"hello","bar":"world"}`);
  assert.equal(JSON.parse(output), input, 'matches original');
});

test.run();
```

Then execute this test file:

```sh
# via `uvu` cli, for all `/tests/**` files
$ uvu -r esm tests

# via `node` directly, for file isolation
$ node -r esm tests/demo.js
```

> **Note:** The `-r esm` is for legacy Node.js versions. [Learn More](/docs/esm.md)

> [View the `uvu` CLI documentation](/docs/cli.md)


## Assertions

The [`uvu/assert`](/docs/api.assert.md) module is _completely_ optional.

In fact, you may use any assertion library, including Node's native [`assert`](https://nodejs.org/api/assert.html) module! This works because `uvu` relies on thrown Errors to detect failures. Implicitly, this also means that any uncaught exceptions and/or unhandled `Promise` rejections will result in a failure, which is what you want!


## API

### Module: `uvu`

> [View `uvu` API documentation](/docs/api.uvu.md)

The main entry from which you will import the `test` or `suite` methods.

### Module: `uvu/assert`

> [View `uvu/assert` API documentation](/docs/api.assert.md)

A collection of assertion methods to use within your tests. Please note that:

* these are browser compatible
* these are _completely_ optional


## Benchmarks

> via the [`/bench`](/bench) directory with Node v14.16.0

Below you'll find each test runner with the following values:

* the `took ___` value is the total process execution time – from startup to termination
* the first parenthesis value (`(___)`) is the self-reported execution time, if known
* the second parenthesis value (`(___)`) is the download size of the NPM module

Each test runner's `stdout` is printed to the console to verify all assertions pass.<br>Said output is excluded below for brevity.

First run:

```
~> "ava"      took 1,080ms  (  ???  )  ( 2,480.00 KiB)
~> "baretest" took    57ms  (  ???  )  (     6.42 KiB)
~> "jasmine"  took    97ms  ( 11.0ms)  (   149.81 KiB)
~> "jest"     took 1,680ms  (616.0ms)  ( 8,350.00 KiB)
~> "mocha"    took   307ms  (  4.0ms)  ( 1,590.00 KiB)
~> "pta"      took   133ms  (  ???  )  (   350.77 KiB)
~> "tap"      took   737ms  (361.1ms)  (16,880.00 KiB)
~> "tape"     took   175ms  (  ???  )  (   568.69 KiB)
~> "test"     took    47ms  (  ???  )  (   159.06 KiB)
~> "uvu"      took    66ms  (  0.8ms)  (   145.04 KiB)
~> "zora"     took    56ms  (  ???  )  (    20.72 KiB)
```

Second run:

```
~> "ava"      took   714ms  (  ???  )
~> "baretest" took    54ms  (  ???  )
~> "jasmine"  took    93ms  ( 11.0ms)
~> "jest"     took 1,170ms  (480.0ms)
~> "mocha"    took   228ms  (  4.0ms)
~> "pta"      took   117ms  (  ???  )
~> "tap"      took   595ms  (344.4ms)
~> "tape"     took   126ms  (  ???  )
~> "test"     took    54ms  (  ???  )
~> "uvu"      took    63ms  (  0.8ms)
~> "zora"     took    54ms  (  ???  )
```

## License

MIT © [Luke Edwards](https://lukeed.com)
