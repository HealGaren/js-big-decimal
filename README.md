# JS Big Decimal

[![Travis](https://img.shields.io/travis/royNiladri/js-big-decimal.svg?style=flat-square)](https://travis-ci.org/royNiladri/js-big-decimal)
[![devDependencies Status](https://david-dm.org/royNiladri/js-big-decimal/dev-status.svg?style=flat-square)](https://david-dm.org/royNiladri/js-big-decimal?type=dev)
[![license](https://img.shields.io/github/license/royNiladri/js-big-decimal.svg?style=flat-square)](https://github.com/royNiladri/js-big-decimal/blob/master/LICENSE)
[![npm](https://img.shields.io/npm/v/js-big-decimal.svg?style=flat-square)](https://www.npmjs.com/package/js-big-decimal)
[![npm](https://img.shields.io/npm/dt/js-big-decimal.svg?style=flat-square)](https://www.npmjs.com/package/js-big-decimal)
<!-- [![Github file size](https://img.shields.io/github/size/royNiladri/js-big-decimal/dist/web/js-big-decimal.min.js.svg?style=flat-square)]() -->

Work with large numbers on the client side with high precision.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Contents

- [Installation](#installation)
  - [Usage](#usage)
- [Operations](#operations)
  - [bigDecimal(number)](#bigdecimalnumber)
  - [getValue()](#getvalue)
  - [getPrettyValue(number, digits, separator)](#getprettyvaluenumber-digits-separator)
  - [round(number, precision)](#roundnumber-precision)
  - [compareTo(number1, number2)](#comparetonumber1-number2)
  - [negate(number)](#negatenumber)
  - [add(augend, addend)](#addaugend-addend)
  - [subtract(minuend, subtrahend)](#subtractminuend-subtrahend)
  - [multiply(multiplicand, multiplier)](#multiplymultiplicand-multiplier)
  - [divide(dividend, divisor, precision)](#dividedividend-divisor-precision)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

---

## Installation
```javascript
npm install --save js-big-decimal
```

### Usage
Require in `javascript` as
```jsavascript
var bigDecimal = require('js-big-decimal');
```
For `typescript`, use
```jsavascript
import bigDecimal require('js-big-decimal');
```
For `web`, when used with script tag, a variable on `Window` object is created.
```html
<script src="node_modules/js-big-decimal/dist/web/js-big-decimal.min.js"></script>
```
```javascript
console.log(bigDecimal.add('12', '45'));
```

## Operations

### bigDecimal(number)
Create a new objet of type BigDecimal. Supports parameters of type `number` and `string`. If string passed cannot be parsed as a number error is thrown. It is recommended to use string as it circumvents the issue of precision with JS native `float` implementation and max limit for `integer`.

It supports exponentiation, but only with integral exponent.

```javascript
var n1 = new bigDecimal(12.6789);
var n2 = new bigDecimal("12345.6789");
var n3 = new bigDecimal('12.456e3'); // 12456
```

### getValue()
Returns the string value of the decimal.
```javascript
console.log(n2.getValue()); // "12345.6789"
```

### getPrettyValue(number, digits, separator)
By default this returns the number in standard number format, comma after every three digts. Both arguments, `digits` - the number of digits (of the integral part) to group by, and `separator` - the character to mark the separation. Example of this can be to format a 16 digit number as _credit card_.
```javascript
var value = bigDecimal.getPrettyValue("12345.6789"); // value = "12,345.6789"
```
Alternately, use the instance property. It returns the result as `string`.
```javascript
var n3 = n2.getPrettyValue(); // n4 = "12,345.6789"

var num = new bigDecimal(1234567890123456)
var card = num.getPrettyValue(4, '-'); // cardNumber = "1234-5678-9012-3456"
```

### round(number, precision)
Returns the rounded value to the specified precision (number of digits after decimal). The default is set to 0 if no argument is passed.
```javascript
var value = bigDecimal.round("123.678", 2); // value = "123.68"
```
Alternately, use the instance property. It returns the result as `bigDecimal`.
```javascript
var n3 = n1.round(2); // n3 = new bigDecimal("12.68")
var n4 = n2.round(); // n4 = new bigDecimal("12346")
```

### compareTo(number1, number2)
Compare two numbers. Returns `1, 0 and -1` if `number1 > number2, number1 == number2 and number1 < number2` respectively.
```javascript
var value = bigDecimal.compareTo("23.678", "67.34"); // value = -1
var value = bigDecimal.compareTo("23.678", "23.6780"); // value = 0
var value = bigDecimal.compareTo("123.678", "67.34"); // value = 1
```
Alternately, use the instance property. It returns the result as `Integer`.
```javascript
var n1 = new bigDecimal('1234');
var n2 = new bigDecimal('8765');
var value = n1.compareTo(n2); // value = -1
```

### negate(number)
Returns negation of a given number.
```javascript
var value = bigDecimal.negate("123.678"); // value = "-123.678";
```
Alternately, use the instance property. It returns the result as new `bigDecimal`.
```javascript
var n = new bigDecimal('-1234');
var value = n.negate(); // value = new bigDecimal('1234')
```

### add(augend, addend)
Add two numbers. Pass in negative for substraction. Ensure parameters are `string`s.
```javascript
var sum = bigDecimal.add("23.678", "67.34"); // sum = "91.018"
var diff = bigDecimal.add("67.34", "-23.678"); // diff = "43.662"
```
Alternately, use the instance property. It returns the result as new `bigDecimal`.
```javascript
var n1 = new bigDecimal('1234');
var n2 = new bigDecimal('8765');
var sum = n1.add(n2); // sum = new bigDecimal('9999')
```

### subtract(minuend, subtrahend)
Subtract one number from another
```javascript
var diff = bigDecimal.subtract("67.34", "23.678"); // diff = "43.662"
```
Alternately, use the instance property. It returns the result as new `bigDecimal`.
```javascript
var n1 = new bigDecimal('12.67');
var n2 = new bigDecimal('130.7');
var diff = n1.subtract(n2); // diff = new bigDecimal('-118.03')
```

### multiply(multiplicand, multiplier)
Multiply two numbers. Ensure parameters are `string`s.
```javascript
var product = bigDecimal.multiply("-0.13", "0.00130"); // product = "-0.000169"
```
Alternately, use the instance property. It returns the result as new `bigDecimal`.
```javascript
var n1 = new bigDecimal('-0.13');
var n2 = new bigDecimal('0.00130');
var product = n1.multiply(n2); // product = new bigDecimal('-0.000169')
```

### divide(dividend, divisor, precision)
Divide two numbers. Pass arguments as `string` if calling on bigDecimal or pass an instance of bigDecimal if calling on object. `precision` is an optional parameter with default value of 8.
```javascript
var quotient = bigDecimal.divide('45', '4', 2); // quotient = 11.25
```
Alternately, use the instance property. It returns the result as new `bigDecimal`.
```javascript
var n1 = new bigDecimal('45');
var n2 = new bigDecimal('4');
var quotient = n1.divide(n2); // quotient = new bigDecimal('11.25')
```
