## 全局对象

当 JS 解释器启动，或浏览器开始加载新页面时，会创建一个全局对象，它包括如下初始属性：

- 全局属性，比如 `undefined`, `Infinity`, `NaN`
- 全局函数，比如 `isNaN()`, `parseInt()`, `eval()`
- 构造函数，比如 `Date()`, `RegExp()`, `String()`, `Object()`, `Array()`
- 全局对象，比如 `Math` 和 `JSON`

用户自定义的全局属性和函数也会作为全局对象的属性。