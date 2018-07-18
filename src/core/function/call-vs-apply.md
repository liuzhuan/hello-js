# call 和 apply 的区别

作用相同，只是调用参数类型不一样。

```js
const a = (x, y) => x + y;

// call 的参数是逗号分隔的不定参数
a.call(null, 2, 3);
// apply 的参数是数组
a.apply(null, [2, 3]);
```