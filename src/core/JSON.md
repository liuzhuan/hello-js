## JSON 对象

JSON 对象包含两个函数：`JSON.stringify()` 和 `JSON.parse()`。

## JSON.stringify()

[mdn](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)

`JSON.stringify()` 方法将一个对象转换为 JSON 字符串。

```js
JSON.stringify(value[, replacer[, space]])
```

其中的 `replacer` 可以是一个函数（用来改变字符串序列化过程），或一个 `String` 或 `Number` 数组（充当白名单，用来过滤字符串序列中显示的属性）。如果该属性为 `null` 或未提供，则 object 的所有属性都会在字符串中出现。

现实世界的[例子](https://github.com/vuejs/vue/blob/dev/src/shared/util.js#L77-L83)：

```js
// vuejs/vue/shared/util.js
export function toString(val) {
    return val == null
    	? ''
    	: typeof val === 'object'
    		? JSON.stringify(val, null, 2)
    		: String(val)
}
```

