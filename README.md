<img align="right" src ="./assets/logo.png" />

# Jewell

Javascript Syntax Sugar for Higher-Order Messaging

[![npm version](https://img.shields.io/npm/v/jewell.svg)](https://www.npmjs.org/package/jewell)
[![Build Status](https://travis-ci.org/pedsmoreira/jewell.svg?branch=master)](https://travis-ci.org/pedsmoreira/jewell)
[![Code Climate](https://codeclimate.com/github/pedsmoreira/jewell/badges/gpa.svg)](https://codeclimate.com/github/pedsmoreira/jewell)
[![Test Coverage](https://codeclimate.com/github/pedsmoreira/jewell/badges/coverage.svg)](https://codeclimate.com/github/pedsmoreira/jewelle/coverage)

Jewell leverages the power of ES6 Proxy to provide syntax sugar, allowing you to write cleaner code.

The best way to showcase Jewell is through code samples:

```javascript
import {jewellPrototype} from 'jewell';
jewellPrototype(Array);

const musics = [...];
musics.forEach.play(); // 💎
musics.forEach(music => music.play()); // Traditional

const animals = [...];
animals.filter.owned.map.name; // 💎
animals.filter(animal => animal.owned).map(animal => animal.name); // Traditional

const employees = [...];
employees.filter.retired.forEach.sendPayment(); // 💎
employees.filter(employee => employee.retired).forEach(employee => employee.sendPayment()); // Traditional
```

## Installation

Using NPM:

```bash
npm install jewell --save
```

Using Yarn

```bash
yarn add jewell
```

Using CDN

```bash
<script src="https://unpkg.com/jewell/dist/index.js"></script>
```

*Note*: You may need an ES6 `Proxy` polyfill to support older browsers.

## API

- `jewell(object: object, propertyName: string)`: Proxies function property. Bear in mind the property must already exist.
- `jewellPrototype(class: object, except: string[])`: Proxies all functions with *zero or one argument* in a class prototype.  

**⚠ Warning**: Be aware that `jewell(...)` and `jewellPrototype(...)` replace the original methods with proxies.
So before you use it in production, make sure you're not creating unintendend behaviors or performance issues.

### Jewelling a property

```javascript
const object = [{name: 'John'}, {name: 'Jane'}];
jewell(object, 'map');
```

### Jewelling a prototype property

```javascript
jewell(Array.prototype, 'map');
```

### Jewelling a class

```javascript
jewellPrototype(Array, ['shift']); // Proxy functions with one or zero args except 'shift
```

## Examples

The examples below expect `jewellPrototype(Array)` to have been called.

### Mapping attributes

```javascript
const fruits = [{name: 'Apple'}, {name: 'Grape'}];
fruits.map.name; // ['Apple', 'Grape']
```

This is the same as `fruits.map(fruit => fruit.name)`.

### Mapping the results of functions

```javascript
const photos = [...];
photos.map.crop(0, 0, 50, 50);
```

### Calling function for each array item

```javascript
const musics = [...];
musics.forEach.play();
```

### Calling function with argument for each array item

```javascript
const photos = [...];
photos.forEach.crop(150, 200);
```

### Filtering items

```javascript
const employees = [...];
employees.filter.retired;
```

### Filtering items with argument

```javascript
const employees = [...];
employees.filter.compliesTo('rule');
```

### Filtering and mapping

```javascript
const animals = [...];
animals.filter.friendly.map.name;
```

### Checking if all items comply to a rule

```javascript
const employees = [...];
employees.every.retired; // true or false
```

### Accessing the original method

The original method is available through `_fn`

```javascript
jewell(array, 'shift');
array.shift._fn // Original method
```

### More examples

If you have some other cool examples, you're very welcome to open a PR.

## Resources

- [Contributing Guide](./CONTRIBUTING.md)
- [Code of Conduct](./CODE_OF_CONDUCT.md)

- The logo was created by Xicons.co and can be found [here](https://www.iconfinder.com/icons/2024653/diamond_gem_jewel_premium_value_icon).

## Motivation

Jewell is inspired by [@franzliedke's implementation](https://laravel-news.com/higher-order-messaging)
of higher-order messaging for [Laravel](http://laravel.com)
and by [Nat Pryce's article](http://natpryce.com/articles/000535.html)
on higher-order messaging with [Ruby](https://www.ruby-lang.org).

Ultimately it would be very nice to have higher-order messaging implemented as a native Javascript feature,
but until then, there's Jewell.

## License

[MIT](./LICENSE)
