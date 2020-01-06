# Method & ES6+ Reference

A reference sheet of some of the most essential JavaScript methods for writing algorithms.

Content adapted from [MDN](https://developer.mozilla.org).

---

## Converting Between Types

### `JSON.stringify`: Object to String

The `JSON.stringify()` method converts a JavaScript object or value to a JSON string, optionally replacing values if a replacer function is specified or optionally including only the specified properties if a replacer array is specified.

```javascript
console.log(JSON.stringify({ x: 5, y: 6 }));
// expected output: "{"x":5,"y":6}"

console.log(
  JSON.stringify([new Number(3), new String('false'), new Boolean(false)])
);
// expected output: "[3,"false",false]"

console.log(JSON.stringify({ x: [10, undefined, function() {}, Symbol('')] }));
// expected output: "{"x":[10,null,null,null]}"

console.log(JSON.stringify(new Date(2006, 0, 2, 15, 4, 5)));
// expected output: ""2006-01-02T15:04:05.000Z""
```

### `parseInt`: String To Integer

The `parseInt()` function parses a string argument and returns an integer of the specified radix (the base in mathematical numeral systems).

```javascript
function roughScale(x, base) {
  const parsed = parseInt(x, base);
  if (isNaN(parsed)) {
    return 0;
  }
  return parsed * 100;
}

console.log(roughScale(' 0xF', 16));
// expected output: 1500

console.log(roughScale('321', 2));
// expected output: 0
```

### `String`: Convert to String

Strings can be created using the String global object directly:
`String(thing)`

### `toString`: Number to String

The toString() method returns a string representing the specified Number object.

**Syntax**
`numObj.toString([radix])`

**Parameters**

`radix`
Optional. An integer in the range 2 through 36 specifying the base to use for representing numeric values.

```javascript
let count = 10;

console.log(count.toString()); // displays '10'
console.log((17).toString()); // displays '17'
console.log((17.2).toString()); // displays '17.2'

let x = 6;

console.log(x.toString(2)); // displays '110'
console.log((254).toString(16)); // displays 'fe'

console.log((-10).toString(2)); // displays '-1010'
console.log((-0xff).toString(2)); // displays '-11111111'
```

_(Note: `toString` is also an object method, although that's a little more complicated.)_

---

## Array/String Methods

### Loops

#### For Loops

```javascript
// Loop through an array
let arr = [1, 2, 3, 4, 5];
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}
// 1
// 2
// 3
// 4
// 5
```

#### `for...of`: Loop through arrays & strings

The `for...of` statement creates a loop iterating over **iterable objects**, including: built-in String, Array, array-like objects (e.g., arguments or NodeList), TypedArray, Map, Set, and user-defined iterables.

It invokes a custom iteration hook with statements to be executed for the value of each distinct property of the object.

```javascript
const array1 = ['a', 'b', 'c'];

for (const element of array1) {
  console.log(element);
}

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

#### `for...in`: Loop through object properties

The `for...in` statement iterates over all enumerable properties of an object that are keyed by strings (ignoring ones keyed by Symbols), including inherited enumerable properties.

It essentially returns the **keys** of an object, but you can easily return the property of an object property like so:

```javascript
const object = { a: 1, b: 2, c: 3 };

for (const property in object) {
  console.log(`${property}: ${object[property]}`);
}

// expected output:
// "a: 1"
// "b: 2"
// "c: 3"
```

#### `forEach`: Loop through arrays

The forEach() method executes a provided function once for each array element.

```javascript
const array1 = ['a', 'b', 'c'];

array1.forEach(element => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

---

## Array Methods

### Fundamentals

#### `filter`

The `filter()` method creates a new array with all elements that pass the test implemented by the provided function.

```javascript
const words = [
  'spray',
  'limit',
  'elite',
  'exuberant',
  'destruction',
  'present'
];

const result = words.filter(word => word.length > 6);

console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

#### `map`

The `map()` method creates a new array populated with the results of calling a provided function on every element in the calling array.

```javascript
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

#### `reduce`

The reduce() method executes a reducer function (that you provide) on each element of the array, resulting in a single output value.

```javascript
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```

#### `sort`

The `sort()` method sorts the elements of an array in place and returns the sorted array. The default sort order is ascending, built upon converting the elements into strings, then comparing their sequences of UTF-16 code units values.

Note: Running the default `sort()` against an array of numbers will sort the numbers according to the first digit of each, rather than the overall value (as seen in the example below)

```javascript
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// expected output: Array ["Dec", "Feb", "Jan", "March"]

const array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);
// expected output: Array [1, 100000, 21, 30, 4]
```

To sort an array of numbers ascendingly:

```javascript
const array1 = [1, 30, 4, 21, 100000];
array1.sort((a, b) => a - b);
console.log(array1);
// expected output: Array [1, 4, 21, 30, 100000]
```

### Algo Essentials

#### `every`

The every() method tests whether all elements in the array pass the test implemented by the provided function. It returns a Boolean value.
**Returns: _Boolean_**

```javascript
const isBelowThreshold = currentValue => currentValue < 40;

const array1 = [1, 30, 39, 29, 10, 13];

console.log(array1.every(isBelowThreshold));
// expected output: true
```

#### `find`

The `find()` method returns the value of the first element in the provided array that satisfies the provided testing function.
**Returns: _value_ of element**

```javascript
const array1 = [5, 12, 8, 130, 44];

const found = array1.find(element => element > 10);

console.log(found);
// expected output: 12
```

#### `findIndex`

The `findIndex()` method returns the index of the first element in the array that satisfies the provided testing function. Otherwise, it returns -1, indicating that no element passed the test.
**Returns: first _index_ (success) or _-1_ (failure)**

```javascript
const array1 = [5, 12, 8, 130, 44];

const isLargeNumber = element => element > 13;

console.log(array1.findIndex(isLargeNumber));
// expected output: 3
```

#### `includes`

The `includes()` method determines whether an array includes a certain value among its entries, returning true or false as appropriate.
**Returns: _boolean_**

```javascript
const array1 = [1, 2, 3];

console.log(array1.includes(2));
// expected output: true

const pets = ['cat', 'dog', 'bat'];

console.log(pets.includes('cat'));
// expected output: true

console.log(pets.includes('at'));
// expected output: false
```

#### `indexOf`

The `indexOf()` method returns the first index at which a given element can be found in the array, or -1 if it is not present.
**Returns: first _index_ (success) or _-1_ (failure)**

### Loops

for...of (array values)
for...in (array indices)

---

## Object Methods

hasOwnProperty
`key` in `object`

---

## String Methods

[MDN Overview (beginner-level)](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Useful_string_methods)
indexOf (first occurrence)
lastIndexOf
replace
replaceAt
startsWith/endsWith
substring

---

## ES6+ Stuff

#### Spread Operator

```javascript
// The ES5 code below uses apply() to compute the maximum value in an array.
var arr = [6, 89, 3, 45];
var maximus = Math.max.apply(null, arr); // 89

// ...arr returns an unpacked array. In other words, it spreads the array.
const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr); // 89

// [...new Set(arr)] = unique value array
const arr = [1, 2, 2, 3, 3, 4, 5, 5];
const uniq = [...new Set(arr)]; // [1,2,3,4,5]

// copy an array
let thisArray = [true, true, undefined, false, null];
let thatArray = [...thisArray];
// thatArray equals [true, true, undefined, false, null]
// thisArray remains unchanged, and is identical to thatArray

// combine arrays
let thisArray = ['sage', 'rosemary', 'parsley', 'thyme'];
let thatArray = ['basil', 'cilantro', ...thisArray, 'coriander'];
// thatArray now equals ['basil', 'cilantro', 'sage', 'rosemary', 'parsley', 'thyme', 'coriander']
```
