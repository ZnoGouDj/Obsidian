Function Composition (композиция)

The function <span style="font-weight: bold; color: mediumvioletred;">compose</span> has a evaluation order from _right to left_:

```javascript
/*
 * 1. take x
 * 2. execute g(x)
 * 3. take the return value of g(x) and execute f with it
*/
const compose = (f, g) => x => f(g(x))
```

There is another function called <span style="font-weight: bold; color: deepskyblue;">pipe</span> which evaluates from _left to right_:

```javascript
const pipe = (g, f) => x => f(g(x))
```

# Function Composition with `n` Arguments

And again we have:
-   <span style="font-weight: bold; color: mediumvioletred;">compose</span>
```js
const compose = (...fns) => fns.reduceRight((f, g) => (...args) => g(f(...args)))
```
-   <span style="font-weight: bold; color: deepskyblue;">pipe</span>
```js
const pipe = (...fns) => fns.reduce((f, g) => (...args) => g(f(...args)))
```

Our goal is it to compose to `ungroup` and `flatten` the function `groupBy`, too.  
We could try

```javascript
const groupByNameAndFlattenAndUngroup = compose(
    flatten,
    ungroup,
    groupBy('name', x)  // <-- this is our problem
)
```

but this will not work. We can only compose functions with one argument. The solution is to rewrite `groupBy` to a _curried_ version:

```javascript
const groupBy = xs => key =>
xs.reduce((rv, x) => {
    (rv[x[key]] = rv[x[key]] || []).push(x)
    return rv
}, {})

const groupByNameAndFlattenAndUngroup = (key, xs) => compose(
    flatten,
    ungroup,
    groupBy ('name')
) (xs)
```

But this solution can be even shorter. If we switch the order of the arguments from `groupBy` to `groupBy = key => xs => {/*..*/}` we can do:

```javascript
const groupBy = key => xs =>
    xs.reduce((rv, x) => {
        (rv[x[key]] = rv[x[key]] || []).push(x)
        return rv
    }, {})

const groupByNameAndFlattenAndUngroup = compose(
    flatten,
    ungroup,
    groupBy ('name')
)
```

# Working Example

```javascript
const arrs = [
  {name: 'abc', effectiveDate: "2016-01-01T00:00:00+00:00"},
  {name: 'abcd', effectiveDate: "2016-02-01T00:00:00+00:00"},
  {name: 'abcd', effectiveDate: "2016-09-01T00:00:00+00:00"},
  {name: 'abc', effectiveDate: "2016-04-01T00:00:00+00:00"},
  {name: 'abc', effectiveDate: "2016-05-01T00:00:00+00:00"},
]

const compose = (...fns) => fns.reduceRight((f, g) => (...args) => 
    g(f(...args)))
    
const ungroup = obj =>
    Object.keys(obj)
        .map(x => obj[x]);

const flatten = arrs =>
    arrs.reduce((acc, item) => acc.concat(item), [])
    
const groupBy = key => xs =>
  xs.reduce((rv, x) => {
      (rv[x[key]] = rv[x[key]] || []).push(x)
      return rv
  }, {})
  
const groupByName = groupBy ('name')
const groupByEffectiveDate = groupBy ('effectiveDate')
  
const groupByNameAndFlattenAndUngroup = compose(
    flatten,
    ungroup,
    groupByName
)

const groupBygroupByEffectiveDateAndFlattenAndUngroup = compose(
    flatten,
    ungroup,
    groupByEffectiveDate
)

console.log(
  groupByNameAndFlattenAndUngroup (arrs)
)

console.log(
  groupBygroupByEffectiveDateAndFlattenAndUngroup (arrs)
)
```