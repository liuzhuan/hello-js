# Sort 排序

数组默认按照 ASCII 字符升序排列，原地排序，并且返回排序后的数组。比如：

```js
var arr = [1, 2, 11, 12, 21, 22];
arr.sort();
// => [1, 11, 12, 2, 21, 22]
```

默认所有的 `undefined` 会排序到最后：

```js
var arr = [1, 2, 3, undefined, 2, undefined];
arr.sort();
// => [1, 2, 2, 3, undefined, undefined]
```

sort 还支持自定义排序规则 `arr.sort(compareFunction)`。元素按照函数返回值进行排序，如果函数的两个参数分别是 `a` 和 `b`：

- 如果 `compareFunction(a, b)` 小于 0，把 `a` 排在 `b` 之前。
- 如果 `compareFunction(a, b)` 等于 0，两者相对位置不变。
- 如果 `compareFunction(a, b)` 大于 0，把 `a` 排在 `b` 之后。

总之，函数值小的在前面。

## 多重排序

如果想对多个字段排序，怎么办？

比如，有如下数组 `arr`，期望首先按照 `age` 降序排列，当 `age` 相同时，再按照 `height` 降序排列。

```js
var arr = [
    { age: 32, height: 188 },
    { age: 42, height: 178 },
    { age: 16, height: 158 },
    { age: 60, height: 188 },
    { age: 32, height: 168 },
]

arr.sort(magicFunction);

// => 
[
    { age: 60, height: 188 },
    { age: 42, height: 178 },
    { age: 32, height: 188 },
    { age: 32, height: 168 },
    { age: 16, height: 158 },
]
```

请问，`magicFunction` 如何编写？

```js
function magicFunction(a, b) {
    if (a.age - b.age !== 0) {
        return b.age - a.age;
    }

    return b.height - a.height;
}
```

如何动态生成这种自定的排序函数？

比如，还是上面的需求。我们期望动态改变排序方式。排序的键值使用 `key` 指定，升降序使用 `asc` 指定（默认为升序，`asc = true`）。

```js
var arr = [...];

const conditions = [
    { key: 'age', asc: false },
    { key: 'height', asc: false },
];
arr.sort(orderBy(conditions));
```

此时 `orderBy` 如何编写？

```js
function orderBy(conditions) {
    return function(a, b) {
        for (let i = 0; i < conditions.length; i++) {
            const { key, asc } = conditions[i];
            const diff = a[key] - b[key];
            if (diff === 0) {
                continue;
            } else {
                return (asc === false) ? -diff : diff;
            }
        }
    }
}
```

## REF

- [Array.prototype.sort() - MDN][mdn]

[mdn]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort