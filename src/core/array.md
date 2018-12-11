# Array 对象

## Array.prototype.reduce()

[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

`reduce()` 函数在数组每个元素执行自定义的 **reducer** 函数，输出是一个元素：

```js
// arr.reduce(callback[, initialValue])
// reducer(accumulator, currentValue, currentIndex, sourceArray)
const array1 = [1, 2, 3, 4]
const reducer = (accumulator, currentValue) => accumulator + currentValue

console.log(array1.reduce(reducer))
// => 10
console.log(array1.reduce(reducer), 5)
// => 15
```

现实世界的[例子](https://github.com/vuejs/vue/blob/d780dd2e2adcf71f40c086055a659a9a2b4a8282/src/shared/util.js#L268)：

```js
// vuejs/vue/src/shared/util.js
function getStaticKeys(modules) {
    return modules.reduce((keys, m) => {
        return keys.concat(m.staticKeys || [])
    }, []).join(',')
}
```

## Array.prototype.concat()

[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Concat)

`concat()` 函数用于合并数组，它不改变原数组，而是返回新数组：

```js
// var new_array = old_array.concat([value1[, value2[, ...[, valueN]]]])
var array1 = ['a', 'b', 'c']
var array2 = ['d', 'e', 'f']

console.log(array1.concat(array2))
// => ["a", "b", "c", "d", "e", "f"]
```
