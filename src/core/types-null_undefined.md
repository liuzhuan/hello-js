## null 和 undefined

`null` 是关键字，表示一个空数值。使用 `typeof` 检测，会返回 `object`：

```javascript
typeof null // => object
```

`undefined` 表示更深层次的“空”。可表示尚未初始化的值，不存在的对象属性，或没有 `return` 语句函数的返回值等。和 `null` 不同，它非关键字，只是一个预定义的全局变量。

ES3 中，`undefined` 可写，能够被替换成任意值。这个错误在 ES5 中得到修正，变为只读。

`undefined` 的类型是 `undefined`：

```javascript
typeof undefined // => undefined
```

尽管略有不同，两者通常可以互用。比如，相等比较运算 `==` 认为他俩是一样的：

```javascript
null == undefined  // => true
null === undefined // => false
```