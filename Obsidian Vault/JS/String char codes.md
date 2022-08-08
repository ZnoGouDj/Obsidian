### [Using charCodeAt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/charCodeAt#using_charcodeat "Permalink to Using charCodeAt()")

The following example returns `65`, the Unicode value for A.

```js
'ABC'.charCodeAt(0)  // returns 65
```

### [Using fromCharCode()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode#using_fromcharcode "Permalink to Using fromCharCode()")

BMP characters, in UTF-16, use a single code unit:

```js
String.fromCharCode(65, 66, 67); // returns "ABC"
```

**!!! Notice** => **charCodeAt** - simp method, so you can use it with **'ABC'.charCodeAt(0)**, and **fromCharCode()** - static, so you use it as **String.fromCharCode(65)**

## Using charAt()

```js
const anyString = 'Brave new world';
console.log(`The character at index 0   is '${anyString.charAt()}'`);
// No index was provided, used 0 as default

console.log(`The character at index 0   is '${anyString.charAt(0)}'`);
console.log(`The character at index 1   is '${anyString.charAt(1)}'`);
```